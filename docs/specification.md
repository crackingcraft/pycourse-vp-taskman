Specification: Task Management System
=====================================

## 1. General Project Description

The Task Management System is a console-based application designed for managing tasks in small projects. It provides a
simple yet effective way to create, view, update, and delete tasks through an interactive command-line interface. The
system is intended as a practical implementation of fundamental programming concepts including data structures, file
I/O operations, user input handling, and basic data manipulation.

The primary goal of this system is to help users organize their tasks efficiently by providing essential task
management functionality with a straightforward interface. It serves as both a useful tool for managing small projects
and an educational example of software development principles.

## 2. Features

### 2.1 Core Features

- **Task Creation**: Users can create new tasks by providing a title, description, priority level, and status.
- **Task Viewing**: Users can view all existing tasks with options for different display formats.
- **Task Updating**: Users can modify any property of an existing task.
- **Task Deletion**: Users can remove tasks from the system.

### 2.2 Advanced Features

- **Data Persistence**: All task data is stored in a text file, ensuring that information persists between sessions.
- **Sorting Capabilities**: Tasks can be sorted by priority or status when viewing.
- **Search Functionality**: Users can search for tasks by keywords in titles or descriptions.

### 2.3 Task Properties

Each task in the system consists of the following properties:

- **Title**: A brief name for the task (text string).
- **Description**: Detailed information about the task (text string).
- **Priority**: The importance level of the task (low, medium, or high).
- **Status**: The current state of the task (new, in progress, or completed).
- **ID**: A unique identifier automatically assigned to each task (integer).

## 3. User I/O

### 3.1 User Interface

The system provides a text-based menu interface that allows users to interact with the application through keyboard
input. The interface is designed to be intuitive and easy to navigate.

### 3.2 Main Menu

Upon starting the application, users are presented with the following options:

```
1. Create a new task
2. View existing tasks
3. Update a task
4. Delete a task
0. Exit the program
```

### 3.3 Task Creation

When creating a new task, the system prompts the user to enter:

- Task title (any text)
- Task description (any text)
- Priority level (low, medium, high)
- Status (new, in progress, completed)

The system automatically assigns a unique ID to the task.

### 3.4 Task Viewing

When viewing tasks, users are presented with additional options:

```
1. Display tasks in original order
2. Sort tasks by status
3. Sort tasks by priority
4. Search tasks by keyword in title or description
```

### 3.5 Task Updating

When updating a task, users are asked to:

1. Enter the ID of the task to update
2. Select which property to update:
    - Title
    - Description
    - Priority
    - Status
3. Enter the new value for the selected property (if no value is entered, the existing value should be preserved)

### 3.6 Task Deletion

When deleting a task, users are asked to enter the ID of the task to delete. The system confirms the deletion and
removes the task from storage.

### 3.7 Input Validation

The system validates user input to ensure that:

- Priority and status selections are within the valid range
- Task IDs exist in the system before updating or deleting
- Required fields are not left empty

## 4. Exchange Data Format

### 4.1 File Storage

All task data is stored in a text file located in the same directory as the application. This ensures data persistence
between sessions.

#### 4.1.1 File Name and Location

- **File Name**: The storage file must be named `tasks.txt`.
- **File Location**: The file must be stored in the same directory as the application main script.
- **File Creation**: If the file does not exist when the application starts, it must be automatically created upon
  the first task addition.

### 4.2 File Format

The system uses a standard CSV (Comma-Separated Values) format for storing task data. This format is straightforward,
human-readable, and easy to process programmatically.

#### 4.2.1 Overall Structure

Each task is stored on a single line in the file. Task properties are separated by a comma (`,`) as a delimiter,
following the standard CSV format. Field values that may contain commas are enclosed in double quotes (`"`) to escape
them.

Example of the file content:

```
1,"Example Task","This is an example task",high,new
2,"Another Task","Description of another task",medium,"in progress"
```

#### 4.2.2 Task Field Structure

Each line in the file represents a single task with fields in the following order:

1. **id**: The unique integer identifier for the task.
2. **title**: The task title.
3. **description**: The task description.
4. **priority**: The priority level ("low," "medium," or "high").
5. **status**: The current status ("new," "in progress," or "completed").

All fields must be present for each task, even if some fields (like description) are empty.

#### 4.2.3 Data Types and Constraints

- **id**: Must be a positive integer.
- **title**: Must be a non-empty string.
- **description**: Must be a string (can be empty).
- **priority**: Must be one of the following strings: "low," "medium," "high."
- **status**: Must be one of the following strings: "new," "in progress," "completed."

#### 4.2.4 Character Encoding and Special Characters

- The file must use UTF-8 encoding to support international characters.
- Field values that contain commas, double quotes, or line breaks must be enclosed in double quotes.
- Double quotes within quoted fields must be escaped by doubling them
  (e.g., `""` represents a single double quote character).
- Only one-line descriptions are acceptable in the basic implementation. Line breaks are not allowed in any field.
- All tasks must be contained on a single line in the file.

### 4.3 Data Loading

When the application starts, it loads all existing tasks from the storage file into memory.

#### 4.3.1 Loading Process

1. The application checks if the storage file exists.
2. If the file exists, the application reads its contents line by line.
3. For each line, the application:
    - Parses the line according to CSV format rules, handling quoted fields and comma delimiters
    - Extracts the five fields (id, title, description, priority, status)
    - Unescapes any special characters in the fields (e.g., converting doubled quotes to single quotes)
    - Creates an in-memory task object with these values
4. If the file does not exist or is empty, the application initializes an empty task collection.

#### 4.3.2 Error Handling During Loading

- If the file exists but a line has an incorrect format (wrong number of fields, invalid data types),
  the application must:
    - Display an error message indicating the problematic line
    - Skip the invalid line and continue processing the rest of the file
    - Log the error for debugging purposes
- If a field contains an invalid value (e.g., invalid priority or status), the application should attempt to use a
  default value and log a warning.

### 4.4 Data Saving

Any changes to tasks (creation, updating, deletion) are immediately saved to the storage file to ensure data integrity.

#### 4.4.1 Saving Process

1. When a task is created, updated, or deleted, the entire collection of tasks is converted to the CSV format.
2. For each task, the application:
    - Encloses fields containing commas, double quotes, or other special characters in double quotes
    - Escapes any double quotes within fields by doubling them
    - Joins the fields with the comma (`,`) delimiter
    - Adds the resulting line to the output
3. The complete text data is written to the storage file, completely replacing its previous contents.

## 5. Acceptance Criteria

The Task Management System must meet the following criteria to be considered complete:

### 5.1 Functionality

- Users must be able to create, view, update, and delete tasks.
- Each task must have a title, description, priority, status, and unique ID.
- Tasks must be sortable by priority and status.
- Users must be able to search for tasks by keywords in titles or descriptions.

### 5.2 Data Persistence

- All task data must be saved to a file and persist between application sessions.
- The system must correctly load existing tasks when started.

### 5.3 User Experience

- The user interface must be intuitive and provide clear instructions.
- The system must validate user input and provide helpful error messages.
- The system must confirm successful operations (task creation, updating, deletion).

### 5.4 Error Handling

- The system must handle invalid user input gracefully.
- The system must handle file I/O errors without crashing.
- The system must provide meaningful error messages to the user.

## 6. Optional Tasks

The following features are not required for the basic implementation but would enhance the system:

### 6.1 Enhanced Task Properties

- **Due Date**: Allow users to set and track deadlines for tasks.
- **Categories/Tags**: Enable users to categorize tasks and filter by categories.
- **Assignee**: Add the ability to assign tasks to different team members.
- **Multiline Descriptions**: Support for multiline text in task descriptions, with proper handling in the CSV file
  format.

### 6.2 Advanced Functionality

- **Batch Operations**: Allow users to update or delete multiple tasks at once.
- **Task Dependencies**: Enable users to define dependencies between tasks.
- **Export/Import**: Add functionality to export tasks to different formats (CSV, JSON) or import from these formats.
- **Statistics**: Provide basic statistics about tasks (e.g., number of completed tasks, tasks by priority).

### 6.3 User Interface Improvements

- **Color Coding**: Use colors in the console to highlight different priorities or statuses.
- **Interactive Selection**: Implement arrow key navigation for menu options.
- **Pagination**: Add pagination for viewing large numbers of tasks.

### 6.4 Command Line Interface (CLI)

Implement a command-line interface with specific commands for task management operations:

#### 6.4.1 Task Creation

```
<program_name> create --title "New task" --desc "Task description" --priority "high"
```

This command creates a new task with the specified title, description, and priority. All parameters are passed as
command-line arguments.

#### 6.4.2 Task Update

```
<program_name> update 2 --status "in_progress"
```

This command updates the task with ID 2, changing its status to "in progress." The first argument is the task ID,
followed by the properties to update.

#### 6.4.3 Task Deletion

```
<program_name> delete 3
```

This command deletes the task with ID 3.

#### 6.4.4 Task Listing

```
<program_name> list
<program_name> list --sort priority
<program_name> list --filter "keyword or phrase"
```

These commands list tasks with various options:

- Without options: lists all tasks
- With `--sort`: sorts tasks by the specified property (e.g., priority)
- With `--filter`: shows only tasks containing the specified keyword or phrase in title or description

#### 6.4.5 Task Details

```
<program_name> get 1
```

This command displays detailed information about the task with ID 1.

## 7. Recommendations

### 7.1 Implementation Approach

It is recommended to follow this implementation order:

1. Design the data structure for storing tasks in memory.
2. Implement core functions for adding, reading, updating, and deleting tasks without user interaction or file
   operations.
3. Create separate functions for each operation and add appropriate validation.
4. Implement sorting and searching functionality.
5. Add file I/O operations for data persistence.
6. Develop the user interface and input handling.
7. Add error handling and user feedback.

### 7.2 Code Organization

- Use constants for values that don't change (e.g., priority levels, status options).
- Create helper functions for common operations (e.g., input validation, ID generation).
- Separate the core functionality from the user interface to improve maintainability.

### 7.3 Testing

- Test each function individually to ensure it works as expected.
- Test the system with various inputs, including edge cases and invalid inputs.
- Verify that data persistence works correctly by restarting the application.

### 7.4 Documentation

- Include comments in the code to explain complex logic.
- Document the data structure and file format used for storing tasks.
- Provide clear instructions for users on how to use the system.
