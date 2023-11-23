# Promise vs Async await
    https://plainenglish.io/blog/differences-between-promises-and-async-await-in-javascript
    
> #### Both Promises and async/await are ways to handle asynchronous operations in JavaScript. They have different syntax

> -    Promises:
>        Promises are objects that represent the eventual completion (or failure) of an asynchronous operation.
>        Promises are created using the new Promise() constructor.
>        Promises can be chained together using the then() and catch() methods.

> -   Async/await:
>        Async/await is a syntax sugar for Promises.
>        Async functions are functions that are marked with the async keyword.
>        Await expressions are expressions that are preceded by the await keyword.

        ```javascript
        const fetchData = (url) => {
            return new Promise((resolve, reject) => {
                fetch(url)
                    .then((response) => {
                        if (!response.ok) {
                            reject(new Error(`HTTP error: ${response.status}`));
                        }
                        return response.json();
                        })
                    .then((data) => resolve(data))
                    .catch((error) => reject(error));
            });
        };

        fetchData('https://jsonplaceholder.typicode.com/todos/1')
            .then((data) => console.log(data))
            .catch((error) => console.error(error));
        ```

        ```javascript
        const fetchData = async (url) => {
            const response = await fetch(url);
            if (!response.ok) {
                throw new Error(`HTTP error: ${response.status}`);
            }
            const data = await response.json();
            return data;
        };

        (async () => {
            try {
                const data = await fetchData('https://jsonplaceholder.typicode.com/todos/1');
                console.log(data);
            } 
            catch (error) {
                console.error(error);
            }
        })();
        ```

> #### Error handling
> With Promises, error handling is typically done using the catch() method. The catch() method is called when the Promise is rejected

> With async/await, error handling is typically done using a try/catch block. The try block contains the asynchronous operation that you want to execute, and the catch block handles any errors that occur.