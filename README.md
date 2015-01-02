Tic-Tac-Toe-Python-
===================
#Initial Board class for Tic-Tac-Toe program

class Board:
    """ a data type for a Tic-Tac-Toe board with arbitrary dimensions """

    def __init__(self, height, width):
        """ a constructor for Board objects """
        self.height = height
        self.width = width
        self.slots = [[' '] * width for r in range(height)]

    def __str__(self):
        """ returns a string representation of a Board """

        s = ''
        
        for row in range(self.height):
            s += '|'
            for col in range(self.width):
                s += self.slots[row][col] + '|'
            s += '\n'

        s += (2 * self.width + 1) * '-'
        s += '\n'

        s += ' '

        for col in range(self.width):
            s += str(col % 10) + ' '

        return s

    def __repr__(self):
        """ returns a string representing the called Board object; allows
            user to evaluate Board object directly from Python Shell and
            have a string be returned that represents the object """

        return self.__str__()

    def add_checker(self, checker, col):
        """ adds the specified checker to column col or the called Board
            object
            input checker: a 1 character string that specifies the checker
                           to add to the board (either 'X' or 'O')
            input col: an int that specifies the index of the column to
                       which the checker should be added and that adds
                       check to the appropriate row in column col of
                       the board """

        row = 0
        while self.slots[row][col] == ' ':
            row += 1
            if row == self.height:
                break
            
        self.slots[row - 1][col] = checker

    def clear(self):
        """ clears the Board object on which it is called by setting all
            slots to contain a space character """

        s = ' '
  
        for row in range(self.height):
            for col in range(self.width):
                self.slots[row][col] = s

    def add_checkers(self, colnums):
        """ takes in a string of column numbers and places alternating
        checkers in those columns of the called Board object, 
        starting with 'X'.
        input colnums: string of alternating column numbers """

        checker = 'X'   # start by playing 'X'

        for col_str in colnums:
            col = int(col_str)
            if 0 <= col < self.width:
                self.add_checker(checker, col)

            # switch to the other checker
            if checker == 'X':
                checker = 'O'
            else:
                checker = 'X' 
            
    def can_add_to(self, col):
        """ returns True if it is valid to place a checker in the column
            col on the calling Board object; otherwise, returns False
            input col: desired column number to place checker in"""

        if col not in range(self.width):
            return False
        if self.slots[0][col] != ' ':
            return False
        else:
            return True

    def is_full(self):
        """ returns True if the called Board object is completely full
            of checkers; otherwise, returns False """


        for col in range(self.width):
            if self.can_add_to(col):
                return False

        return True

    def remove_checker(self, col):
        """ removes the top checker from column col of the called Board
            object; if column is empty, then function should do nothing
            input col: specified column number to remove checker from """

        row = 0
        
        while self.slots[row][col] == ' ':
            row += 1
            if row == (self.height):       
                row -= 1
                break
            
     
        self.slots[row][col] = ' '


    def is_horizontal_win(self, checker):
        """ Checks for a horizontal win for the specified checker. """
    
        for row in range(self.height):
            for col in range(self.width - 3):
            # Check if the next four columns in this row
            # contain the specified checker.
                if self.slots[row][col] == checker and \
                   self.slots[row][col + 1] == checker and \
                   self.slots[row][col + 2] == checker:
                    return True

    def is_vertical_win(self, checker):
        """ Checks for a vertical win for the specified checker """
         
        for row in range(self.height - 2):
            for col in range(self.width):
                if self.slots[row][col] == checker and \
                   self.slots[row + 1][col] == checker and \
                   self.slots[row + 2][col] == checker:
                    return True

    def is_up_diagonal_win(self, checker):
        """ Checks for an up diagonal win for the specified checker """
        for row in range(self.height - 1, 3, -1):
            for col in range(self.width - 3):
        # Check if rows leading up diagonally
        # contain the specified checker.
                if self.slots[row][col] == checker and \
                   self.slots[row - 1][col + 1] == checker and \
                   self.slots[row - 2][col + 2] == checker:
                    return True

    def is_down_diagonal_win(self, checker):
        """ Checks for a down diagonal win for the specified checker """
        for row in range(self.height - 3):
            for col in range(self.width - 3):
        # Check if rows leading down diagonally
        # contain the specified checker.
                if self.slots[row][col] == checker and \
                   self.slots[row + 1][col + 1] == checker and \
                   self.slots[row + 2][col + 2] == checker:
                    return True

    def is_win_for(self, checker):
        """ accepts a parameter checker that is either 'X' or 'O'; returns True
            if there are four consecutive slots containing checker on the board;
            otherwise, returns False """

        if self.is_horizontal_win(checker):
            return True
        if self.is_vertical_win(checker):
            return True
        if self.is_up_diagonal_win(checker):
            return True
        if self.is_down_diagonal_win(checker):
            return True

        return False
    
        #checker - either 'X' or 'O'
