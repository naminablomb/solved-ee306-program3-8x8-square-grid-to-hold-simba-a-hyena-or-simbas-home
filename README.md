Download Link: https://assignmentchef.com/product/solved-ee306-program3-8x8-square-grid-to-hold-simba-a-hyena-or-simbas-home
<br>
The purpose of this assignment is to write, load and display a grid  in LC-3 assembly language. The grid here is  a 8×8 square of spaces where each space can hold Simba, a Hyena, or Simba’s Home. In this programming assignment, you will learn to write code that interfaces with pre-written code. This program is part of a sequence that will eventually result in a game called<em> Save Simba</em>​           ​. You will use both Array and Linked-list data structures in the coding of this program.

Details

The ​<em>Save Simba game </em>​involves a jungle made up of a grid of squares (aka <em>gridblocks</em>​         ​). For this assignment, the jungle is a 8×8 grid. The ​<em>Initial </em>​and ​<em>Home </em>​locations  along with locations of the ​<em>Hyenas </em>are loaded as input to the game. The input is structured as a ​<strong>linked-list</strong>​. Your job is to complete 3 subroutines that load the jungle information (LOAD_JUNGLE), display the Jungle (DISPLAY_JUNGLE) and convert grid coordinates to an address (GRID_ADDRESS).




Input

The input is a linked list of records representing ​<em>gridblocks </em>​with 3 ​<em>fields</em>​:

<ul>

 <li>a ​<em>link </em>​to the next record</li>

 <li>coordinates (row, col) each ranging [0, 7]</li>

 <li>a character indicating ​<em>gridblock </em>​type

  <ul>

   <li>I​ (<em>Initial</em>​ ​)</li>

  </ul></li>

</ul>

○ H​ (​<em>Home</em>​) ○ #​ (​<em>Hyena</em>​)

<u>Note</u>​: Each record contains a field that is the address to the next record. This field is called a ​<em>link</em>​, which gives this data structure its name, ​<strong>linked-list</strong>. The last record will have a ​           ​<em>link </em>​field with an address of ​x0000​. This is the sentinel that signals the end of the linked list.

An example input file (​Jungle.asm​) is provided in the starter code. In ​Jungle.asm​, instead of scattering the linked list all over different parts of memory, all records are stored in a single file linked using labels instead of addresses. This is done for convenience; your code must work even if the linked list records are scattered across memory.

<u>Notes</u>​:

<ul>

 <li>The ​<strong>address </strong>​of the ​<strong>first </strong>​record in the list will be stored in x5000. (The first record is not at x5000). This address is referred to as the ​<strong>head </strong>​of the list.</li>

 <li>There is no defined order in which these records occur. For example, it is possible for the ​<em>Home </em>record to be at the head of the linked list.</li>

 <li>There will only be one ​<em>Initial </em>​gridblock and one ​<em>Home </em>​gridblock in the list. You do not have to do any error checking.</li>

 <li>There may be zero or more ​<em>Hyena </em>​ If there are no records with ​#​ in them, then that means there are no Hyenas in the jungle.</li>

 <li>When processing the list you need to pay special attention to the ​<em>Initial </em>​and ​<em>Home </em>​records:

  <ul>

   <li>For the​ ​<strong><em>Initial </em></strong>​gridblock, you need to put an ​ ​<strong>*​</strong> in the corresponding entry in the ​GRID​ and set the global variables ​CURRENT_ROW​ and CURRENT_COL​​ (More on these variables below.)</li>

  </ul></li>

</ul>

○ For the ​<strong><em>Home</em></strong>​ ​gridblock, you need to put an​ ​<strong>H​</strong> in the corresponding entry in the ​GRID and set the global variables ​HOME_ROW​ and ​HOME_COL​ accordingly. (More on these variables below.)

You need to follow all these rules (listed above) for processing the input data when writing your subroutine called ​LOAD_JUNGLE​.




GRID

The Jungle ​GRID​ is a 4×4 grid of spaces defined initially as shown in the left figure of the following table.

<table width="542">

 <tbody>

  <tr>

   <td width="266">          0​ 1 2 3 4 5 6 7+-+-+-+-+-+-+-+-+         0 | | | | | | | | |​                   +-+-+-+-+-+-+-+-+         1 | | | | | | | | |​                         +-+-+-+-+-+-+-+-+         2 | | | | | | | | |​                         +-+-+-+-+-+-+-+-+         3 | | | | | | | | |​                         +-+-+-+-+-+-+-+-+         4 | | | | | | | | |​                         +-+-+-+-+-+-+-+-+         5 | | | | | | | | |​                         +-+-+-+-+-+-+-+-+         6 | | | | | | | | |​                         +-+-+-+-+-+-+-+-+         7 | | | | | | | | |​+-+-+-+-+-+-+-+-+</td>

   <td width="276">          0​ 1 2 3 4 5 6 7+-+-+-+-+-+-+-+-+         0 | | | | | | | | |​                  +-+-+-+-+-+-+-+-+         1 | | | | | | | | |​             +-+-+-+-+-+-+-+-+         2 | | | | | | | | |​                   +-+-+-+-+-+-+-+-+         3 | | | | | | | | |​                   +-+-+-+-+-+-+-+-+         4 | | | | | | | | |​                   +-+-+-+-+-+-+-+-+         5 | | | | | | | | |​                   +-+-+-+-+-+-+-+-+         6 | | | | | | | | |​                   +-+-+-+-+-+-+-+-+         7 | | | | | | | | |​+-+-+-+-+-+-+-+-+</td>

  </tr>

  <tr>

   <td width="266">Initial</td>

   <td width="276">After Load</td>

  </tr>

 </tbody>

</table>

The ​GRID​ itself is a set of ​.STRINGZ​ declarations without the row and column numbers (numbers in pink, above). For example, after loading an input linked list with a ​<em>Initial </em>​location at (2, 1); a ​<em>Home </em>​location at (1, 2); and three Hyenas at (0, 2), (1, 1), and (3, 1); the GRID looks like the right figure above.

Pre-written Code

The main program that is the engine of your game is provided to you along with the declaration of the GRID​ and several variables.







<h1>Your Task / Subroutines</h1>

Implement the following ​<strong>three </strong>subroutines. Two of these subroutines are called by my code, the other​   (​GRID_ADDRESS​) is a utility routine that is called by your code. We will test it though.

<ul>

 <li><strong>DISPLAY_JUNGLE​</strong>: This subroutine displays the state of the ​GRID ​to the Console.</li>

</ul>

○ Inputs: None

○ Outputs: None

The jungle GRID is located in memory at the label ​GRID​. It is simply a set of .stringz declarations:

GRID .STRINGZ “+-+-+-+-+-+-+-+-+”

.STRINGZ “| | | | | | | | |”

.STRINGZ “+-+-+-+-+-+-+-+-+”

.STRINGZ “| | | | | | | | |”

.STRINGZ “+-+-+-+-+-+-+-+-+”

.STRINGZ “| | | | | | | | |”

.STRINGZ “+-+-+-+-+-+-+-+-+”

.STRINGZ “| | | | | | | | |”

.STRINGZ “+-+-+-+-+-+-+-+-+”

.STRINGZ “| | | | | | | | |”

.STRINGZ “+-+-+-+-+-+-+-+-+”

.STRINGZ “| | | | | | | | |”

.STRINGZ “+-+-+-+-+-+-+-+-+”

.STRINGZ “| | | | | | | | |”

.STRINGZ “+-+-+-+-+-+-+-+-+”

.STRINGZ “| | | | | | | | |”

.STRINGZ “+-+-+-+-+-+-+-+-+”




Note that each string is null-terminated. The output is not just a simple print of these strings as can be seen in the figure above. Each column and row number are indicated (shown in pink above) in the display of the grid on the console. You can create your own .STRINGZ  for column numbers, if you need. ​<strong>You are NOT allowed to modify the GRID or any code provided to you</strong>​.

<ul>

 <li><strong>LOAD_JUNGLE​</strong>: This subroutine reads the input linked list and appropriately populates the contents of the jungle GRID​​      . See above for the description of the input format.

  <ul>

   <li>Inputs: ​R0​ – the address of the head of the linked list of gridblock records</li>

  </ul></li>

</ul>

○ Outputs: None

○ Purpose: Populates the ​GRID​ with the appropriate characters (​*​, ​H​, ​#​) Additionally, set the following variables:

■ CURRENT_ROW​ – initialize with the row of the ​<em>Initial </em>​gridblock

■ CURRENT_COL​ – initialize with the column of the ​<em>Initial </em>​gridblock

■ HOME_ROW​ – initialize with the row of the ​<em>Home </em>​gridblock

■ HOME_COL​ – initialize with the column of the ​<em>Home </em>​gridblock

<ul>

 <li><strong>GRID_ADDRESS​</strong>: This subroutine is a key subroutine that both your code and eventually the game itself depends on. It translates the (row, col) logical GRID​​ coordinates of a gridblock to the physical address in the ​GRID​

  <ul>

   <li>Inputs: ​R1​ – row number [0, 7]; ​R2​ – column number [0, 7]</li>

  </ul></li>

</ul>

○ Outputs: ​R0​ – corresponding memory address of the gridblock in the ​GRID Hint: There are 17 physical rows of characters and only 8 logical rows.







<h1>Sample Run</h1>

Here is the console output of a sample run of a working solution:




0 1 2 3 4 5 6 7

+-+-+-+-+-+-+-+-


<ul>

 <li>| | | | | | | | |</li>

</ul>

+-+-+-+-+-+-+-+-


<ul>

 <li>| | | | | | | | |</li>

</ul>

+-+-+-+-+-+-+-+-


<ul>

 <li>| | | | | | | | |</li>

</ul>

+-+-+-+-+-+-+-+-


<ul>

 <li>| | | | | | | | |</li>

</ul>

+-+-+-+-+-+-+-+-


<ul>

 <li>| | | | | | | | |</li>

</ul>

+-+-+-+-+-+-+-+-


<ul>

 <li>| | | | | | | | |</li>

</ul>

+-+-+-+-+-+-+-+-


<ul>

 <li>| | | | | | | | |</li>

</ul>

+-+-+-+-+-+-+-+-


<ul>

 <li>| | | | | | | | |</li>

</ul>

+-+-+-+-+-+-+-+-





Jungle Initial







0 1 2 3 4 5 6 7

+-+-+-+-+-+-+-+-


<ul>

 <li>| |#| | | | | | |</li>

</ul>

+-+-+-+-+-+-+-+-


<ul>

 <li>| |#| | | | | | |</li>

</ul>

+-+-+-+-+-+-+-+-


<ul>

 <li>| |*| | | | | | |</li>

</ul>

+-+-+-+-+-+-+-+-


<ul>

 <li>| | | | | |#| | |</li>

</ul>

+-+-+-+-+-+-+-+-


<ul>

 <li>| | | | |#| | |H|</li>

</ul>

+-+-+-+-+-+-+-+-


<ul>

 <li>| | | | | | |#| |</li>

</ul>

+-+-+-+-+-+-+-+-


<ul>

 <li>| | | |#| | | | |</li>

</ul>

+-+-+-+-+-+-+-+-


<ul>

 <li>| | | | | | | | | +-+-+-+-+-+-+-+-+</li>

</ul>




Jungle Loaded




—– Halting the processor —–







The top of the output  shows the console with the initial state of the jungle before it is populated. The second part shows the console after the jungle is populated and the program halted.