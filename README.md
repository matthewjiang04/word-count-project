def count_words(source_file):
    '''
    Purpose: Count how many of each word appear in a file
    Parameter(s):
        source_file: the file that is being counted for number of words
    Return Value:
        A dictionary of words followed by how many times they appear in the source file. (dict)
    '''

    fp = open(source_file, 'r')
    count = {}
    for line in fp:
        words = line.split()
        for word in words:
            try:
                number = count[word]
                count[word] = number+1
            except:
                count[word] = 1
    fp.close()
    return count
if __name__ == '__main__':

    print(count_words('short1.txt'))
    #{'Never': 3, 'gonna': 3, 'give': 1, 'you': 2, 'up.': 1,
    #'let': 1, 'down.': 1, 'run': 1, 'around': 1, 'and': 1,
    #'desert': 1, 'you.': 1}

    print(count_words('short2.txt'))
    #{'Fear': 2, 'is': 1, 'the': 2, 'path': 1, 'to': 4,
    #'dark': 1, 'side.': 1, 'leads': 3, 'anger.': 1, 'Anger': 1,
    #'hate.': 1, 'Hate': 1, 'suffering.': 1, 'I': 1,
    #'sense': 1, 'much': 1, 'fear': 1, 'in': 1, 'you.': 1}

import random
def weighted_choice(counts):
    '''
    Purpose: Take in a dictionary of words and numbers and randomly chooses a word in the dictionary according to the number of times it appears. 
    Parameter(s):
        counts: a dictionary of a word and a number count for that word. (dict)
    Return Value:
        Returns a random word in the dictionary that is weighted by its number count. (str)
    '''
    all_words = []
    for words in counts:
        for num in range(counts[words]):
            all_words.append(words)
    word = random.choice(all_words)
    return word
if __name__ == '__main__':
    results = []
    for i in range(600):
        item = weighted_choice({'green': 1, 'eggs': 3, 'ham':2})
        results.append(item)
    print(results.count('green')) #about 100
    print(results.count('eggs')) #about 300
    print(results.count('ham')) #about 200

def random_sent(source_file, num_words):
    '''
    Purpose:
        Randomly generate a new sentence using the words in a file containing a paragraph
    Parameter(s):
        source_file: The file containing the words that will be used for new sentence
        num_words: The number of words that will be in the newly generated sentence. (int)
    Return Value:
        Returns a new randomly generated sentence. (str)
    '''

    random_sentence = ''
    word_count = count_words(source_file)
    for words in range(num_words):
        random_sentence += weighted_choice(word_count) + ' '
    return random_sentence

if __name__ == '__main__':
    print()
    print(random_sent('short3.txt', 10))
    
    print()
    print(random_sent('hamlet.txt', 20))
    
    print()
    print(random_sent('alice.txt', 30))
