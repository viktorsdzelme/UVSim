UVSim README
============

Description
-----------
UVSim is a Python implementation of the BasicML virtual machine.
It loads a BasicML program into memory and executes the instructions until a HALT instruction is reached.
This version includes a Graphical User Interface (GUI) to simplify loading, editing, and running programs.

Requirements
------------
- Python 3
- tkinter (This is included with standard Python 3 installations, so no additional third-party modules or pip installs are required)

Running the Program
--------------------
To launch the GUI, run the following from the command line:
    python gui.py

GUI Controls (User Manual)
---------------------------
Load File
    Opens a file browser so the user can select a BasicML program from any folder on the computer.
    The file opens in a new tab. If the file is already open, its existing tab is selected instead
    of opening a duplicate.

Save
    Saves the currently active tab's program back to the file it was loaded from.

Save As
    Saves the currently active tab's program under a new file name and/or in a different folder.
    The tab's title updates to reflect the new file name.

Convert to 6-Digit
    Converts the currently active tab's program from 4-digit BasicML instruction format to 6-digit
    format, inserting the extra opcode/operand digits for recognized instructions, so it can be
    edited and saved as a 6-digit program.

Close File
    Closes the currently active tab, after asking the user to confirm. Any unsaved changes in that
    tab are discarded.

Set Colors
    Opens the system color picker so the user can choose a primary color and an off-color for the
    interface. Two color picker dialogs are shown in sequence: one for the primary color, then one
    for the off-color. Each dialog opens already showing the current color as the default selection.

    Colors are specified using Hex RGB notation (the same format used for colors on the web, e.g. in
    HTML/CSS). Within the color picker dialog, the Hex field shows the current default value and can
    be used to enter a color directly. A valid Hex RGB value:
        - Must start with a "#" character.
        - Is followed by exactly 6 hexadecimal digits (0-9 and A-F), two digits each for the
          red, green, and blue components.
        - Each pair ranges from 00 (none of that color) to FF (full intensity of that color).

    Examples:
        #FFFFFF   -> white
        #000000   -> black
        #4C721D   -> UVU green (the application default primary color)

    If you're not familiar with Hex RGB notation, a quick reference and color picker is available at
    https://www.w3schools.com/colors/colors_picker.asp

    Which controls are affected:
        - Primary Color sets the background of the main window and of the top-level frames/
          containers (for example, the row of buttons along the top of the window).
        - Off Color is used in two places: as the text (foreground) color for labels and buttons
          sitting on the primary-color background, and separately as the background color of the
          program editor boxes and the Output box. Text inside the editor and Output boxes always
          stays black, regardless of the colors chosen.

    The selected colors are saved in uvsim_colors.txt and loaded automatically the next time the
    program starts.

Program Code / Memory (tabs)
    Each loaded file opens in its own tab, with its own editor box, so multiple programs can be open
    and edited at the same time.
    Within a tab, users may add, edit, and delete BasicML instructions directly by typing in the
    editor box. Cut, copy, and paste are done using the standard operating system keyboard shortcuts
    (e.g. Ctrl+X, Ctrl+C, Ctrl+V on Windows/Linux, or Cmd+X, Cmd+C, Cmd+V on macOS) - there are no
    separate on-screen cut/copy/paste buttons. Undo (Ctrl+Z) is also supported within a tab's editor.

Run Selected Program
    Runs the program in the currently active tab.
    If the program in the editor is longer than 250 lines, the GUI displays a warning that the
    program exceeds 250 lines, and only the first 250 lines are loaded into memory and executed;
    the remaining lines are ignored for that run.

Output
    Displays the results of write instructions and the final execution status/message for the most
    recently run program.

Command Line Usage
-------------------
You can still run the simulator from the command line:
    python unified_structure.py <program_file>

Example:
    python unified_structure.py Test1.txt

If no file is provided, the program will prompt:
    Enter the path to the BasicML program file:

Program Input/Output (Command Line)
-------------------------------------
When a READ instruction is executed, the simulator prompts:
    Enter a word (signed 4-digit integer):

Inputs must be integers between -9999 and 9999.

When a WRITE instruction is executed, output is displayed as a signed 4-digit word, such as:
    +0027
    -0150

Included Test Files
---------------------
Test1.txt: Prompts for two values, adds them together, prints the result, and halts.
Test2.txt: Prompts for two values, compares them, prints the larger value, and halts.
Test3.txt, Test3b.txt, Test4.txt, Test5.txt: Additional test cases covering branching, division, multiplication, and various scenarios.

Color Configuration
---------------------
By default, UVSim uses the official UVU color scheme.

Primary Color:
    #4C721D
Off-Color:
    #FFFFFF

Users may change these colors using the Set Colors button, which opens the system color picker.
The selected colors are stored in:
    uvsim_colors.txt

The application automatically loads the saved colors when it starts.

Running Unit Tests
--------------------
Run all unit tests with:
    python -m unittest test_uvsim.py
