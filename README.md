# word-search
class Solution(object):
    def exist(self, board, word):
        """
        :type board: List[List[str]]
        :type word: str
        :rtype: bool
        """
        if not board or not board[0]:
            return False

        rows, cols = len(board), len(board[0])

        def dfs(r, c, idx):
            # If all characters matched
            if idx == len(word):
                return True

            # Out of bounds or character mismatch
            if r < 0 or r >= rows or c < 0 or c >= cols or board[r][c] != word[idx]:
                return False

            # Mark the cell as visited
            temp = board[r][c]
            board[r][c] = '#'

            # Explore 4 directions
            found = (dfs(r+1, c, idx+1) or
                     dfs(r-1, c, idx+1) or
                     dfs(r, c+1, idx+1) or
                     dfs(r, c-1, idx+1))

            # Restore the cell
            board[r][c] = temp
            return found

        for i in range(rows):
            for j in range(cols):
                if board[i][j] == word[0] and dfs(i, j, 0):
                    return True

        return False
