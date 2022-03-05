# #520 Detect Capital

> We define the usage of capitals in a word to be right when one of the following cases holds:

> All letters in this word are capitals, like "USA".
> All letters in this word are not capitals, like "leetcode".
> Only the first letter in this word is capital, like "Google".

> Given a string word, return true if the usage of capitals in it is right.

#### Technique

Okay. Before beginning to code, lets look at the accepted cases versus rejection cases for this problem.

There are three cases for which our function should return True.

1. The word has all capitals.
2. The word has all lower case letters.
3. The word starts with 1 capital followed by all lowercase letters.

Automatically, I understand what is False:

1. Any word that has capital letters for the first two letters, followed by lower case letters is False. **ex: LIzardpeople**
2. Any word that begins with a lower case letter contains any capital letters, it is False. **ex: lizardPeople**
3. Any word that has a capital letter followed by a lower case letter contains another capital letters, it is False. **ex: LiZARDPEOplE**

Like an artist using negative space to structure a painting, I will use the False cases to define my function.

#### Code

```java
    public boolean detectCapitalUse(String word) {
    if(word.length() == 1){
        return true;
    }
    if(Character.isUpperCase(word.charAt(0)) && Character.isUpperCase(word.charAt(1))){
        for(int i = 2; i<word.length(); i++){
            if(Character.isLowerCase(word.charAt(i))){
                return false;
            }
        }
    }else if(Character.isLowerCase(word.charAt(0))){
        for(int i = 1; i<word.length(); i++){
            if(Character.isUpperCase(word.charAt(i))){
                return false;
            }
        }
    }else if(Character.isUpperCase(word.charAt(0)) && Character.isLowerCase(word.charAt(1))){
        for(int i = 2; i<word.length(); i++){
            if(Character.isUpperCase(word.charAt(i))){
                return false;
            }
        }
    }
    return true;

}
```

###### Block by block explanation

- ```Java
     if(word.length() == 1){
        return true;
    }
  ```

  A catch case: if the word consists of one letter, all cases are true by default. **ex: A, a**
  <br />

- ```Java
     if(Character.isUpperCase(word.charAt(0)) && Character.isUpperCase(word.charAt(1))){
        for(int i = 2; i<word.length(); i++){
            if(Character.isLowerCase(word.charAt(i))){
                return false;
            }
        }
  ```

  False statement number 1. If the word begins with 2 uppercase letters, the word should contain no lower case letters. If a lower case is found, return False. **Ex: QUeenelizabeth**
  <br />

- ```Java
   else if(Character.isLowerCase(word.charAt(0))){
        for(int i = 1; i<word.length(); i++){
            if(Character.isUpperCase(word.charAt(i))){
                return false;
            }
        }
  ```
  False statement number 2. If the word begins with a lower case letters but contains an uppercase letter, return False. **ex: queenElizabeth**
  <br />
- ```Java
    else if(Character.isUpperCase(word.charAt(0)) && Character.isLowerCase(word.charAt(1))){
        for(int i = 2; i<word.length(); i++){
            if(Character.isUpperCase(word.charAt(i))){
                return false;
            }
        }
  ```

  False statement number 3. IF the word begins with an upper case letter, followed by a lower case letter, but contains yet another upper case letter, return False. **ex: QuEenElizabeth**
  <br />

- `return true;`
  Finally, if none of the above cases returned False, return True. Meaning word satisfies all the true cases. **ex: QueenElizabeth, QUEENELIZABETH, queenelizabeth**
