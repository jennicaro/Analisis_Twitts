# Analisis_Twitts

projectTwitterDataFile = open("project_twitter_data.csv","r")
resultingDataFile = open("resulting_data.csv","w")
punctuation_chars = ["'", '"', ",", ".", "!", ":", ";", '#', '@']
# lists of words to use
positive_words = []
with open("positive_words.txt") as pos_f:
    for lin in pos_f:
        if lin[0] != ';' and lin[0] != '\n':
            positive_words.append(lin.strip())
def get_pos(positive_wordx):
    positive_wordx= strip_punctuation(positive_wordx)
    good_words= positive_wordx.split()
   
    
    count_pst=0
    for word in good_words:
        word= word.lower()
        for words in positive_words:
            words=words.lower()
            if word == words:
                count_pst+=1
    return count_pst

negative_words = []
with open("negative_words.txt") as pos_f:
    for lin in pos_f:
        if lin[0] != ';' and lin[0] != '\n':
            negative_words.append(lin.strip())

def get_neg(negative_wordsx):
    negative_wordsx= strip_punctuation(negative_wordsx)
    negative_list=negative_wordsx.split()
    
    count_neg=0
    for nword in negative_list:
        nword= nword.lower()
        for nxword in negative_words:
            nxword=nxword.lower()
            if nword == nxword:
                count_neg+=1
    return count_neg

def strip_punctuation(my_string):
    for punctuation in punctuation_chars:
        my_string= my_string.replace(punctuation, "")
    return my_string

def writeInDataFile(resultingDataFile):
    resultingDataFile.write("Number of Retweets, Number of Replies, Positive Score, Negative Score, Net Score")
    resultingDataFile.write("\n")

    linesPTDF =  projectTwitterDataFile.readlines()
    headerDontUsed= linesPTDF.pop(0)
    for linesTD in linesPTDF:
        listTD = linesTD.strip().split(',')
        resultingDataFile.write("{}, {}, {}, {}, {}".format(listTD[1], listTD[2], get_pos(listTD[0]), get_neg(listTD[0]), (get_pos(listTD[0])-get_neg(listTD[0]))))    
        resultingDataFile.write("\n")

        

writeInDataFile(resultingDataFile)
projectTwitterDataFile.close()
resultingDataFile.close()
