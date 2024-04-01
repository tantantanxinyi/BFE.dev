# Decode message

The link: https://bigfrontend.dev/problem/decode-message

You'r are given a 2-D array of characters. There is a hidden message in it.

```
I B C A L K A
D R F C A E A
G H O E L A D
```

The way to collect the message is as follows
1. start at top left
2. move diagonally down right
3. when cannot move any more, try to switch to diagonally up right
4. when cannot move any more, try switch to diagonally down right, repeat 3
5. stop when cannot neither move down right or up right. the character on the path is the message
for the input above, IROCLED should be returned.

notes:
if no characters could be collected, return empty string


```
 const message = [
   ['I', 'B', 'C', 'A', 'L', 'K', 'A'],
   ['D', 'R', 'F', 'C', 'A', 'E', 'A'],
   ['G', 'H', 'O', 'E', 'L', 'A', 'D']
 ];
```


direction:
 [+1, +1]  right down
 [+1, -1]  right up

 In this problem,  the x-axis direction will  always be  from left to right, we don't need to handle the direction on x-axis,  we just need to keep track of the  vertical direction whether it's up or down. We can use the while loop to loop through from  first column to last column.

 We can start from row 0 and column 0, and we need to descend to right by incrementing the row and the column, if we arrive at the last row, meaning there is no next row exists, so we need to change the vertical direction to ascend to  right by decrementing the row and incrementing the column, and finally, we will stop at the last column. 

 If the message.length equals 0 , we need to return empty string.  If the message[0].length is 0, indicating that no elements exits,  then we need to return empty string as well.

```
function decode(message){
  if(message.length === 0) return "" 
  if(message[0].length === 0 ) return ""
}
```

 We define the  variable result  to collect the character letter, and we need to store the column length and row length. The inital vertial direction is positive 1 which means the direction is  going down.

```
function decode(message){
  if(message.length === 0) return "";
  if(message[0].length === 0 ) return "";

  const rows = message.length;
  const cols = message[0].length;

  let row = 0; // current row index
  let col = 0; // current column index
  let directionY = 1;  // to update the vertial direction.
  let result = ""; // to collect the character letters.

  while (col < cols && row > -1 && row < rows){
    // meaing this column is available
    results += message[row][col] //collect current character

    row += directionY; // to update the row,
    col += 1; // the direction of column always be right

    if(row > rows -1){
      // meaning that we reached the row boundary, we need to reverse the direction
      directionY = -1;
      row -= -2  // subtract two
    }else if(row < 0){
      directionY = 1;
      row += 2
    }
  }
  return result;
}
```