class Solution:
    def maxScoreWords(self, words: List[str], letters: List[str], score: List[int]) -> int:        
        def dfs(i, starting_budget, path_score):
            '''
            Choose the max out of all paths' scores (a path is a distinct combination of words) - make sure a path is valid by keeping track of our budget
            i: index of current word, starting_budget: budget we have when arriving at this word, path_score: current accumulated path's score
            '''
            # Base case: we've fully completed a path
            if i == N: # Indicated by index out of range
                self.res = max(self.res, path_score) # Update our result - choosing the larger between the score of previous path & current path
                return # End of path, nothing more to do, just return
            
            # Decision to include the current word or not - If the 'cost' of current word exceeds the budget -> NOT INCLUDE, else INCLUDE
            to_include = True # Set the decision to True initially
            remaining_budget = starting_budget.copy() # The remaining budget if we decide to include current word
            for letter in words[i]: # For each letter of the current word
                remaining_budget[letter] -= 1 # "Pay the price" of that letter
                if remaining_budget[letter] < 0: # If the budget of that letter exceeded
                    to_include = False # Decide NOT to include current word
                    break # No need to pay the remaining letters as we're broke already
            
            # If we decide to include the current word, then proceed with next word, with the remaining budget, and with added current word's score to current path's score
            if to_include:
                dfs(i + 1, remaining_budget, path_score + self.word_scores[i]) # Include current & search for next
            # Always inspect the case where we don't include current word despite the decision above, it may lead to a larger path's score even if the budget for current word is enough
            dfs(i + 1, starting_budget, path_score) # Not include current & search for next (proceed with the budget that hasn't been subtracted, and not added current word's score)

        N = len(words)
        
        # 1. Create an array to store each words[i]'s score
        self.word_scores = [] # Array
        for word in words: # For each words[i]
            word_score = 0 # Score of words[i]
            for letter in word: # For each character in words[i]
                word_score += score[ord(letter) - 97] # Accumulate the score
            self.word_scores.append(word_score) # Append to the array
        
        # 2. Create a HashMap counting frequencies of `letters`, this is also our `original_budget`
        original_budget = Counter(letters)
        
        # 3. Start DFS & Backtracking
        self.res = 0 # Initialize our result variable
        dfs(0, original_budget, 0) # Call DFS on the first word (words[0]) with i=0, starting_budget=original_budget, res=0
        return self.res # Return final result
