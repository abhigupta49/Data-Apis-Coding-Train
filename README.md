
# fetch() - Working With Data & APIs in JavaScript

The Fetch API provides a JavaScript interface for accessing and manipulating parts of the HTTP pipeline, such as requests and responses.



## First Way



```javascript
  fetch('https://image.shutterstock.com/image-vector/rainbow-arc-shape-half-circle-260nw-1111672163.jpg').then(res=>{
    console.log(res);
    return res.blob()
}).then(res=>{
    console.log(res)
    document.getElementById('rainbow').src = URL.createObjectURL(res)
}).catch(err=>{
    console.log(err)
})
```

## Second Way

-The async and await keywords enable asynchronous, promise-based behavior to be written in a cleaner style, avoiding the need to explicitly configure promise chains.

```javascript
  async function catchRainbow(){
    const response = await fetch('https://image.shutterstock.com/image-vector/rainbow-arc-shape-half-circle-260nw-1111672163.jpg');
    const blob = await response.blob();
    document.getElementById('rainbow').src = URL.createObjectURL(blob)
    
    console.log(response)
    
}
catchRainbow().then(response=>{
    console.log('yay');
}).catch(error=>{
    console.log(error);
})
```