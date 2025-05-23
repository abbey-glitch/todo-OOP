[![Deploy static content to Pages](https://github.com/abbey-glitch/todo-OOP/actions/workflows/static.yml/badge.svg)](https://github.com/abbey-glitch/todo-OOP/actions/workflows/static.yml)


*Overview*
A simple yet functional Todo List application with alarm functionality built using Object-Oriented Programming in JavaScript. The app allows users to add tasks with specific due times and notifies them with an alarm sound when tasks are due.

*Features*
Add Todos: Create new todo items with description and due time

Alarm Notifications: Audio alarm and browser alert when task time arrives

*Task Management:*

Mark tasks as complete/incomplete

*Delete tasks*

Persistent Storage: Todos are saved in browser's localStorage

Responsive Design: Clean, mobile-friendly interface

*Installation*
No installation required! This is a client-side web application that runs directly in the browser.

Download the HTML file (todo.html)

Open it in any modern web browser

*Usage*
Add a new todo:

Enter task description in the text field

Select date and time using the datetime picker

Click "Add" button

Manage todos:

Click "Complete" to mark a task as done (click again to undo)

Click "Delete" to remove a task

Alarms:

When a todo's time arrives:

An alarm sound will play

A browser alert will appear asking if you want to mark the task as complete

*Technical Details*
Programming Paradigm: Object-Oriented JavaScript

Classes:

TodoItem: Represents individual todo items

TodoList: Manages the collection of todos (Singleton pattern)

Storage: Uses browser's localStorage for persistence

Dependencies: None (pure JavaScript, no frameworks)

Customization
You can easily customize:

Alarm sound by replacing the audio file URL

Styling by modifying the CSS in the 

Alarm behavior by editing the triggerAlarm method

*Limitations*
Requires modern browser with localStorage support

Audio alarm may be blocked by browser autoplay policies (user interaction required first)

Not designed for mobile notifications when browser is closed

*Future Enhancements*
Recurring todos

Multiple alarm sounds

Push notifications

Category/tag system

Sync across devices

*License*
Free to use and modify. Audio alarm is from SoundJay.
