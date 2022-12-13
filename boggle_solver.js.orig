/**
 * Represents a book.
 * @constructor
 * @param {string} word -
 * @param {trie} trie -
 */
function isValidWord(word, trie) {
  return trie[word] === 1;
}

/**
 * // checks for valid prefix
 * @constructor
 * @param {string} word -
 * @param {trie} trie -
 */
function isValidPrefix(word, trie) {
  return trie[word] != undefined;
}

/**
 * // checks for valid grid
 * @constructor
 * @param {grid} grid - The title of the book.
 */
function isValidGrid(grid) {
  // grid must be of size NxN
  N = grid.length;

  // letters in grid must match the following regex
  const regex = /(st|qu)|[a-prt-z]/;

  for (let i = 0; i < N; i++) {
    if (grid[i].length !== N) {
      return false;
    }

    for (let j = 0; j < grid[i].length; j++) {
      if (!grid[i][j].toLowerCase().match(regex)) {
        return false;
      }
    }
  }

  return true;
}

/**
 * // checks for valid grid
 * @constructor
 * @param {number} size -
 *
//function getVisitedGrid(size) {
  const visited = [];
  for (let i = 0; i < size; i++) {
    currentRow = [];
    for (let j = 0; j < size; j++) {
      currentRow.push(false);
    }
    visited.push(currentRow);
  }
  return visited;
}/*/

/**
 * // get trie from dict
 * @constructor
 * @param {dict} dictionary -
 */
function getTrieFromDictionary(dictionary) {
  const dict = {};

  for (let i = 0; i < dictionary.length; i++) {
    const currentWord = dictionary[i].toLowerCase();
    const currentWordLength = currentWord.length;

    dict[currentWord] = 1;

    for (let j = currentWordLength; j > 1; j--) {
      prefix = currentWord.substr(0, j - 1);
      if (prefix in dict) {
        if (dict[prefix] == 1) {
          dict[prefix] = 1;
        }
      } else {
        dict[prefix] = 0;
      }
    }
  }


  return dict;
}

// adjecent tiles
const adjcaentTiles = [
  [-1, -1], [-1, 0], [-1, 1],
  [0, -1], [0, 1],
  [1, -1], [1, 0], [1, 1],
];
/**
 * // find words funtion
 * @constructor
 * @param {grid} grid -
 * @param {trie} trie -
 * @param {int} i -
 * @param {int} j -
 * @param {string} visited -
 * @param {string} solutions -
 * @param {string} currentString -
 */
function findWords(grid, trie, i, j, visited, solutions, currentString) {
  // search tile is out of grid
  if (i < 0 || j < 0 || i >= grid.length || j >= grid.length) {
    return;
  }

  // We have already used this cube to form a word. Ignore it
  if (visited[i][j] == true) {
    return;
  }

  const newString = (currentString + grid[i][j]).toLowerCase();

  if (isValidPrefix(newString, trie)) {
    visited[i][j] = true;

    if (isValidWord(newString, trie)) {
      if (newString.length >= 3) {
        solutions.add(newString);
      }
    }

    for (let x = 0; x < adjcaentTiles.length; x++) {
      const nextTile = adjcaentTiles[x];
      findWords(grid, trie, i + nextTile[0], j + nextTile[1],
          visited, solutions, newString);
    }
  }

  visited[i][j] = false;
}


exports.findAllSolutions = function(grid, dictionary) {
  let solutions = [];

  // check if the grid and dictionary is passed
  if (grid == null || dictionary == null) {
    return [];
  }

  // if dictionary is empty, there are no valid words that we can generate
  if (dictionary.length == 0) {
    return [];
  }

  // check if the grid is correct
  if (!isValidGrid(grid)) {
    return [];
  }

  // using set to remove duplicate words from boggle
  const solutionSet = new Set();
  const trie = getTrieFromDictionary(dictionary);

  // Iterate over each cube in the grid as the starting letter for a word
  for (let i = 0; i < grid.length; i++) {
    for (let j = 0; j < grid[i].length; j++) {
      // Maintain a list of tiles that have been used
      // for form a word since it cannot be reused twice
      const visited = Array(grid.length).fill().map(() =>
        Array(grid.length).fill(false));

      findWords(grid, trie, i, j, visited, solutionSet, '');
    }
  }

  // change set to array
  solutions = Array.from(solutionSet);
  return solutions;
};

const grid = [['t', 'w', 'y', 'r'],
  ['e', 'n', 'p', 'h'],
  ['g', 'z', 'qu', 'r'],
  ['o', 'n', 't', 'a']];
const dictionary = ['art', 'ego', 'gent', 'get', 'net', 'new', 'newt', 'prat',
  'pry', 'qua', 'quart', 'quartz', 'rat', 'tar', 'tarp',
  'ten', 'went', 'wet', 'arty', 'egg', 'not', 'quar'];


console.log(exports.findAllSolutions(grid, dictionary));
