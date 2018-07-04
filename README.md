# Frequency analysis of english letters in literature masterpieces

import pprint

LETTERS = 'abcdefghijklmnopqrstuvwxyz'

def histogram(stringS):
    diction = dict()
    for c in stringS:
        c = c.lower()
        if c in LETTERS:
            if c not in diction:
                diction[c] = 1
            else:
                diction[c] += 1
    return diction

def totalNumber(someDict):
    num = 0
    for value in someDict.values():
        num += value
    return num

def calculatePercent(n, someDict):
    newHist = {}
    for k, v in someDict.items():
        newHist[k] = round((v / n * 100), 2)
    return newHist

def getFreqOrder(someDict):
    freqToLetter = {}
    for letter in LETTERS:
        if someDict[letter] not in freqToLetter:
            freqToLetter[someDict[letter]] = letter
    return freqToLetter

def getItemAtIndexZero(x):
    return x[0]

def freqPairs(someDict):
    freqPairs = list(someDict.items())
    freqPairs.sort(key=getItemAtIndexZero, reverse=True)
    return freqPairs

def main():
    for i in ['alice.txt', 'siddhartha.txt', 'moby_dick.txt', 'gatsby.txt']:
        filename = i
        try:
            with open(filename) as f_obj:
                contents = f_obj.read()
        except FileNotFoundError:
            msg = 'Sorry, the ' + filename +  ' does not exist.'
            print(msg)
        else:
            hist = histogram(contents)

        totalNum = totalNumber(hist)
        newDict = calculatePercent(totalNum, hist)
        freqDict = getFreqOrder(newDict)

        nList = freqPairs(freqDict)
                           
        with open('frequency_analysis.txt', 'a') as file_obj:
            file_obj.write('Вот частота букв английского алфавита в процентах в произведении "%s" :\n' % filename)
            for k in nList[:6]:
                file_obj.write('{}\n'.format(k))

    print('All results are written in the file "frequency_analysis.txt"!')
      
if __name__ == '__main__':
    main()


    

    









