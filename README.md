## Curiosity Marsbot Remote Operation

The Curiosity Marsbot, operating on Mars, is controlled remotely by programmers on Earth. By sending control codes from a matrix keyboard, the programmer directs the movement of the Marsbot as follows:

### Control Codes and Their Meaning

| Control Code | Meaning |
|--------------|---------|
| `1b4`        | Marsbot starts moving |
| `c68`        | Marsbot stops |
| `444`        | Turn left 90 degrees from the current direction |
| `666`        | Turn right 90 degrees from the current direction |
| `dad`        | Start leaving tracks |
| `cbc`        | Stop leaving tracks |
| `999`        | Automatically retrace the route in reverse. No tracks are left, and no other commands are accepted until the reverse route is completed. Description: The Marsbot is programmed to remember the entire history of control codes and the intervals between each change in command. This allows it to reverse its route and return to the starting point. |

### Command Activation

After receiving the control codes, Curiosity Marsbot does not process them immediately; it waits for a command activation signal from the Keyboard & Display MMIO Simulator. There are three such commands:

| Activation Key | Meaning |
|----------------|---------|
| `Enter`        | Ends code input and commands Marsbot to execute |
| `Delete`       | Clears all control codes currently being entered |
| `Space`        | Repeats the last executed command |

### Task

Write a program that allows Marsbot to operate as described. Additionally, add a feature where each time a control code is sent to Marsbot, the code is displayed on the console so that observers can monitor the vehicle's route.

## Key Functions of the Program

1. **Keyboard Scanning**: The program scans the keyboard to receive control commands from the user. When a command is detected, it performs the corresponding actions associated with that command.

2. **Robot Control**: Based on the commands from the keyboard, the program performs actions such as moving, turning left, turning right, stopping, etc.

3. **Storing the Robot's Path**: When the robot performs an action (such as moving or turning), its new position and direction are stored in a path array. This allows the program to track and record the routes the robot has taken.

4. **Drawing the Robot's Path**: When needed, the program can toggle the mode to draw the robot's path. When this mode is enabled, the robot will leave a trace on the surface as it moves.

5. **Error Notification**: If the program receives an invalid command from the keyboard, it will notify the user of the error.

6. **Interrupt Handling**: The program handles interrupt events, which in this case occur when receiving an event from the keyboard.

7. **Defined Constants and Addresses**: The program defines several constants and addresses, including the ASCII codes for keyboard keys and the addresses of the robot's control ports.

8. **Memory Management**: The program uses operations to manage memory, including storing and accessing variables and arrays.

### Constants and Variable Definitions

- The `.eqv` directives are used to define constants, making it easier to change their values.
- Variables such as `inputControlCode`, `lengthControlCode`, `nowHeading`, `path`, and `lengthPath` are declared to store and manage data during the program's execution.

### Main Function

- It begins by initializing the registers `$k0` and `$k1` with the respective values of the addresses related to the keyboard.
- Next, it enables the keyboard interrupt and then enters an infinite loop to wait for a keypress.

### Helper Functions

- Functions like `GO`, `STOP`, `TRACK`, `UNTRACK`, `ROTATE`, `removeControlCode`, `isEqualString`, `pushErrorMess`, and others are used to control the robot and process data from the keyboard.
- These functions perform tasks such as controlling the robot's movement, storing data, deleting data, comparing strings, and notifying errors.

### Interrupt and Interrupt Handling

- The `.ktext` section defines the interrupt handling functions.
- Each interrupt handling function performs a specific task, such as scanning the keyboard matrix, retrieving the ASCII code of the pressed key, storing the code in the `inputControlCode` variable, and finally returning to the main program for further processing.

### Other Subroutines

- There are subroutines like `storePath`, `goBack`, `goRight`, `goLeft`, `removeControlCode`, `isEqualString`, `pushErrorMess` to perform specific tasks and help clarify the program code.
