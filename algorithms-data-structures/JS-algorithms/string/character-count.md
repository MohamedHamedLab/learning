- Write a function which takes in a string and return back count each character in the string
- if character not a string don't do anything
- 
  **examples**
  ```js
  chartCount("aaaaa") //{a:4}
  chartCount("hello") // {h1:, e1, l2: o1: }
  chartCount("hello hi!") // {21:, e: 1, l: 2: o: 1, i:1 }
  ```

  **function**
 
```js
function isValidAnagram(str1,str2) {
    if(str1.length !== str2.length){
        return false
    }
    const lookup = {}
    for (let i=0; i < str1.length; i++) {
        let letter = str1[i]
        lookup[letter]  ? lookup[letter] +=1 :  lookup[letter] = 1
     }
     for(let i=0; i < str2.length; i++) {
      let letter = str2[i]
         if(!lookup[letter]){
            return false  
         }else{
            lookup[letter] -= 1 
         }
     }
    return true
}


test('Anagrams', () => {
    expect(isValidAnagram("","")).toBeTruthy()
    expect(isValidAnagram("aaz","zaa")).toBeTruthy()
    expect(isValidAnagram("texttwisttime","timetwisttext")).toBeTruthy()
    expect(isValidAnagram("rat","car")).toBeFalsy()
});
```