# AutoQuery - Search Query Autocomplete System

This project is a C++ implementation of a search query autocomplete system designed for search engines. It suggests up to three of the most frequent and lexicographically ordered queries that match the user's current input in real-time. The suggestions are based on previously entered sentences and their respective frequencies.

## Features

1. **Dynamic Autocomplete**: As the user types, the system suggests the top 3 sentences that match the prefix of the current query.
2. **Historical Query Tracking**: Every sentence entered by the user, ending with the special character `#`, is stored along with its usage frequency.
3. **Efficient Search**: The system uses a Trie (prefix tree) to store and retrieve sentences efficiently, providing real-time query suggestions.
4. **Frequency and Lexicographical Ordering**: Suggestions are primarily sorted by frequency, and when two sentences have the same frequency, they are ordered lexicographically using ASCII values.
5. **Adaptive Learning**: Each new query updates the system’s knowledge, influencing future suggestions.

## Assumptions

- Users can input sentences that may contain multiple words, ending with a special character `#`.
- For every character typed (excluding `#`), the system returns up to the top 3 sentences that start with the same prefix.
- If there are fewer than 3 matching sentences, the system returns as many as possible.
- The frequency of a sentence increases every time the user inputs that exact sentence.
- Input consists of lowercase letters (`a` to `z`), spaces (` `), and the special character `#`. When `#` is entered, the sentence is saved, and the system resets to handle new input.

## Key Methods

### `AutoCompleteSystem`

Constructor for initializing the system. Accepts two inputs:

- `sentences`: A list of strings representing previously typed sentences.
- `times`: A list of integers representing the number of times each sentence was previously typed.

### `input(char c)`

Handles each character input by the user. 

- If the input is a character (letters or space), the system provides suggestions for the top 3 sentences that match the prefix typed so far.
- If the input is `#`, the current sentence is stored and the system resets for a new query.

## Example

```cpp
AutoCompleteSystem obj({"i love icecream", "island", "ironman", "i love football"}, {5, 3, 2, 2});
```

This initializes the system with the following historical data:
- `"i love icecream"`: typed 5 times
- `"island"`: typed 3 times
- `"ironman"`: typed 2 times
- `"i love football"`: typed 2 times

### Sample User Interactions

#### Example 1:
```cpp
obj.input('i');
```
**Output**:
```text
["i love icecream", "island", "i love football"]
```
Explanation: There are four sentences starting with the prefix `"i"`. Based on frequency and lexicographical order, "ironman" is excluded, and the top 3 suggestions are shown.

#### Example 2:
```cpp
obj.input(' ');
```
**Output**:
```text
["i love icecream", "i love football"]
```
Explanation: There are only two sentences that start with `"i "`, so only two suggestions are shown.

#### Example 3:
```cpp
obj.input('a');
```
**Output**:
```text
[]
```
Explanation: No sentences match the prefix `"i a"`, so the system returns an empty list.

#### Example 4:
```cpp
obj.input('#');
```
**Output**:
```text
[]
```
Explanation: The input `"i a"` is saved in the system as a new sentence, and the input is reset.

## Time Complexity

- **Insertion and Lookup**: The expected time complexity for each input query is **O(n * max|L|)**, where:
  - `n` is the number of historical sentences stored.
  - `L` is the maximum length of a sentence.

## Project Tags

- **Data Structures**: Tries, Priority Queues
- **Algorithm Design**: Prefix Matching, Lexicographical Ordering
- **System Design**: Autocomplete, Query Suggestion System
- **Programming**: C++, Strings

## Use Cases

- **Search Engines**: Provide real-time query suggestions based on user input.
- **Text Editors**: Suggest previously typed phrases or commands for faster text entry.
- **E-Commerce Platforms**: Assist users in typing popular search queries for products.

This system demonstrates the power of using data structures like Tries combined with priority queues to build efficient, responsive autocomplete functionality.
