Part-A:
We can use a pressure-sensitive resistor matrix arranged in an 8×8 matrix, where each square detects pressure changes when a piece is lifted or placed. This setup can detect "lift" (piece removed) and "place" (piece set down) events without cameras or tags.
Component layout: 1)Grid Matrix Structure:Place a sandwich of conductive and resistive layers under each square:
																					Top layer: Conductive row lines.
																					Middle layer: Pressure-sensitive material.
																					Bottom layer: Conductive column lines.
																					This forms an 8×8 matrix = 64 intersections, each representing one square.
								  2) Microcontroller Interface:
																					Use a matrix scanning method with a microcontroller (like Arduino):
																					8 output pins (rows) and 8 input pins (columns) = 16 total pins.
									3) Data Acquisition:
																					Scan each row sequentially and read the pressure values across columns.
																					Use analog reads (if resistive sensors) or digital thresholding (if tactile switches or FSRs with defined outputs).
                                            <table>
                                              <tr>
                                                <td>Event Type</td>
                                                <td>Detected As</td>
                                              </tr>
                                              <tr>
                                                <td>Piece Lifted</td>
                                                <td>Pressure drops to 0</td>
                                              </tr>
                                              <tr>
                                                <td>Piece Placed</td>
                                                <td>Pressure rises</td>
                                              </tr>
                                              </table>
												
By comparing the state difference between two scans, we can detect:
From square: Where pressure dropped (lifted).
To square: Where pressure increased (placed).
<img src="https://github.com/PriyanshuJ26/Awesome_Robotics_Club_PriyanshuJoshi_240806/blob/main/solution.png"/>

Part-B:
Our goal is to detect which of the 64 squares (8×8) has gone from 0 → 1 (piece lifted) using minimal I/O pins, for which we will be using 16 pins (8 rows + 8 columns).
The concept is matrix scanning using wires for rows and columns.Imagine the 64 squares as forming an 8×8 matrix.Each square is connected at an intersection of a row and a column wire.We don’t need individual wires for each square.
Rows (R0–R7): 8 output pins
Columns (C0–C7): 8 input pins
Total pins: 16
Each square contains a normally open switch (or any component that gives a HIGH signal on lift).
Working:
a)Drive one row LOW at a time, and keep all other rows HIGH or in high impedance (input mode).
b)Read all columns:If a switch is pressed (activation), the corresponding column will read LOW.
c)Repeat for all rows.
This way, any activation is detected as a coordinate (row, column).
    C0   C1   C2   C3   C4   C5   C6   C7
   -------------------------------------
R0 | o — o — o — o — o — o — o — o     ← drive LOW
R1 | o — o — o — o — o — o — o — o
R2 | o — o — o — o — o — o — o — o
R3 | o — o — o — o — o — o — o — o
R4 | o — o — o — o — o — o — o — o
R5 | o — o — o — o — o — o — o — o
R6 | o — o — o — o — o — o — o — o
R7 | o — o — o — o — o — o — o — o

