- Write a function to determine if the second string is anagram of the first

**example**
isValidAnagram("","") // true
isValidAnagram("aaz","zza") // true
isValidAnagram("rat","car") // false
isValidAnagram("texttwisttime","timetwisttext") // true


**Function**
```jsx
function isValidAnagram(str1,str2) {
    if(str1.length !== str2.length){
        return false
    }
    const lookup = {}
    for (let val of str1) {
        let letter = str1[val]
        lookup[letter] = lookup[letter] ? lookup[letter]+ 1:  1
     }
      for (let val of str2) {
      let letter = str2[val]
         if(lookup[letter]){
            lookup[letter] -= 1  
         }else{
             return false
         }
     }
    return true
}


test('Anagrams', () => {
    expect(isValidAnagram("","")).toBeTruthy()
    expect(isValidAnagram("texttwisttime","timetwisttext")).toBeTruthy()
    expect(isValidAnagram("aaz","zaa")).toBeTruthy()
    expect(isValidAnagram("rat","car")).toBeFalsy()
});
```