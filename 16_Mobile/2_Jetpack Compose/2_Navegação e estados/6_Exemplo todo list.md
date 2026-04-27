
```kotlin

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContent {
            TodoListTheme {
                TodoListScaffold()
            }
        }
    }
}


@Composable
fun TodoListScaffold() {
    var showDialog by remember { mutableStateOf(false) }
    Scaffold(
        floatingActionButton = { AddTaskFloatingButton({ showDialog = true }) },
        modifier = Modifier.fillMaxSize()
    ) { innerPadding ->
        TodoMainScreen(
            dialogIsVisible = showDialog,
            toggleDialog = { showDialog = !showDialog },
            modifier = Modifier.padding(innerPadding)
        )
    }
}


@Composable
fun AddTaskFloatingButton(openDialog: () -> Unit) {
    FloatingActionButton(
        onClick = openDialog,
    ) {
        Icon(
            imageVector = Icons.Filled.Add,
            contentDescription = stringResource(R.string.add_task_fab_content_description)
        )
    }
}

@Composable
fun TodoMainScreen(dialogIsVisible: Boolean, toggleDialog: () -> Unit, modifier: Modifier = Modifier) {
    val todos = remember { mutableStateListOf(*tasks.toTypedArray()) }
    val selectedCategories = remember { mutableStateSetOf<String>() }

    val filteredTodos by remember {
        derivedStateOf {
            if (selectedCategories.isEmpty()) {
                todos.toList()
            } else {
                todos.filter { it.category.name in selectedCategories }
            }
        }
    }

    Column(
        horizontalAlignment = Alignment.CenterHorizontally,
        modifier = modifier
    ) {
        val sizeOfCategories = Category.values().size
        MultiChoiceSegmentedButtonRow(
            modifier = Modifier.fillMaxWidth().padding(horizontal = 4.dp)
        ) {
            Category.values().forEachIndexed { index, category ->
                val selected = selectedCategories.contains(category.name)
                SegmentedButton(
                    shape = SegmentedButtonDefaults.itemShape(
                        index = index,
                        count = sizeOfCategories
                    ),
                    checked = selected,
                    onCheckedChange = {
                        val constantName = category.name
                        if (it) selectedCategories.add(constantName) 
                        else selectedCategories.remove(constantName)
                    },
                    label = {
                        Text(text= category.label )
                    },
                    icon = { SegmentedButtonDefaults.Icon(selected) },
                )
            }
        }
        LazyColumn(
            horizontalAlignment = Alignment.Start,
            modifier = Modifier
                .fillMaxSize()
                .padding(10.dp)
        ) {
            items(
                items = filteredTodos,
                key = { it.id }
            ) { todo ->
                TodoItem(todo, modifier = Modifier.animateItem())
            }
        }
    }

    AnimatedVisibility(visible = dialogIsVisible) {
        AddTaskDialog(
            onDismiss = toggleDialog,
            onConfirm = { task ->
                todos.add(task)
                toggleDialog()
            }
        )
    }
}

@Composable
fun TodoItem(task: Task, modifier: Modifier = Modifier) {
    var checked by remember { mutableStateOf(task.done) }
    Row(
        verticalAlignment = Alignment.CenterVertically,
        modifier = modifier
    ) {
        val color = when(task.category) {
            Category.SAUDE -> Color.Green
            Category.ESTUDO -> Color.Blue
            Category.ESPORTE -> Color.Cyan
            Category.LAZER -> Color.Magenta
        }
        Checkbox(
            checked = checked,
            onCheckedChange = { checked = it },
            colors = CheckboxDefaults.colors(
                uncheckedColor = color,
                checkedColor = color
            )
        )
        Text(
            text = task.description,
            fontSize = 24.sp
        )
    }
}

@Preview
@Composable
fun PreviewTodoItem() {
    TodoItem(
        Task(
            description = stringResource(R.string.preview_task_description),
            category = Category.SAUDE,
            done = true
        )
    )
}

@Preview(showBackground = true)
@Composable
fun TodoMainScreenPreview() {
    TodoListTheme {
        TodoListScaffold()
    }
}
```