exports.findAllSolutions = function(grid, dictionary) {
  let solutions = [];

  //check if inputs are valid, if invalid return [] 
  if (grid == null || dictionary == null) {
    return solutions;
    }

  //check if NxN
  let N = grid.length;
  for (let i = 0; i < N; i++) {
    if (grid[i].length != N) {

    return solutions;
    }
  }

  //convert input to lowercase
  lowerCase(grid, dictionary);


  //check if grid is valid
  if (!validGrid(grid)) {
    console.log('TEST: ' + grid);
    return solutions;
  }
  
  //set up all data structures 

  let setSolution = new Set();
  let hash = hashmap(dictionary);

  //iterate over NxN grid, find all words that begin with grid[y][x]
  for (let y = 0; y < N; y++) {
    for (let x = 0; x < N; x++) {
      let word = '';

      let used = new Array(N).fill(false).map(() => new Array(N).fill(false));

      wordSearch(word, y, x, grid, used, hash, setSolution);
    }
  }
  
  solutions = Array.from(setSolution);
  
  return solutions;
}


validGrid = function(grid) {
  reg_ex = /(st|qu)|[a-prt-z]/;
  for (let i = 0; i < grid.length; i++) {
    for (let j = 0; j < grid[i].length; j++) {
      if (!grid[i][j].match(reg_ex)) {
        return false;
      }
    }
  }
  return true;
}

lowerCase = function(grid, dict) {
  for (let i = 0; i < grid.length; i++) {
    for (let j = 0; j < grid.length; j++) {
      grid[i][j] = grid[i][j].toLowerCase();
    }
  }
  
  for (let i = 0; i < dict.length; i++) {
    dict[i] = dict[i].toLowerCase();
  }
}
hashmap = function(dictionary) {
  var dict= {};
  for (let i = 0; i < dictionary.length; i++) {
    dict[dictionary[i]] = 1;
    let wordLength = dictionary[i].length;
    var str = dictionary[i];
    for (let j = wordLength; wordLength > 1; wordLength--) {
      str = str.substr(0,wordLength-1);
      if (str in dict) {
        if (str == 1) {
          dict[str] = 1;
        }
      }
      else {
          dict[str] = 0;
      }
    }
  }
  return dict;
}
wordSearch = function(word, y, x, grid, used, hash, setSolution) {

  let adj_matrix = [[-1, -1],
                    [-1, 0],
                    [-1, 1],
                    [0, 1],
                    [1, 1],
                    [1, 0],
                    [1, -1],
                    [0, -1]];

  //base case:
  //b1: y and x out of bounds
  //b2: already used y and x
  //return 

  if (y < 0 || x < 0 || y >= grid.length || x >= grid.length || used[y][x] == true) 
    return;

  //append grid[y][x] to word
  word += grid[y][x];

  
  //is it a prefix for any word already in hash

  if (is_prefix(word, hash)) {
  //is the prefix a complete word in dictionary
    used[y][x] = true;
    
  //if length >= 3 add word to setSolution
    if (isWord(word, hash)) {
      if (word.length >= 3)
        setSolution.add(word);
    }

  //keep call wordSearch()
    for (let i = 0; i < 8; i++) {
      wordSearch(word, y + adj_matrix[i][0], x + adj_matrix[i][1], grid, used, hash, setSolution);
    }
  }
  
  //if not prefix then unmark y,x as used
  used[y][x] = false;
}

//helper functions

is_prefix = function(word, hash) {
  return hash[word] != undefined;
}

isWord = function(word, hash) {
  return hash[word] == 1;
}
//
//
var grid = [['T', 'W', 'Y', 'R'],
            ['E', 'N', 'P', 'H'],
            ['G', 'Z', 'Qu', 'R'],
            ['St', 'N', 'T', 'A']];

var dictionary = ['art', 'ego', 'gent', 'get', 'net', 'new', 'newt', 'prat',
                  'pry', 'qua', 'quart', 'quartz', 'rat', 'tar', 'tarp',
                  'ten', 'went', 'wet', 'arty', 'egg', 'not', 'quar'];
console.log(exports.findAllSolutions(grid, dictionary));
