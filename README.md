# AsyncRequest

RESTful Promise-based AJAX requests

## Introduction

AsyncRequest gives you a more modern way to write your AJAX requests.

I have made this for my [camagru](https://github.com/jeremie-gauthier/camagru) project because I wanted a cleaner way to make AJAX requests.

Here are the features:

- **GET**/**POST**/**PUT**/**DELETE** requests
- **async**/**await** notation
- send data in **JSON**

## Getting started

Just include the AsyncRequest.js where you want to use it.

```html
<script type="text/javascript" src="AsyncRequest.js"></script>
```

## Promise-based

Each method return a **Promise** that resolves when the request finished and the response is ready.

## Example With POST (client-side)

```js
const login = async () => {
  try {
    const url = "api/auth/login";
    const data = { ... };
    const headers = {
      "Content-type": "application/x-www-form-urlencoded"
    };

    await AsyncRequest.post(url, data, headers);
  } catch (err) {
    // handle error
  }
}
```

## Example With POST (server-side)

I will show you a way to handle the above request in **PHP** as this was the mandatory language for my project.

```php
if ($_SERVER["REQUEST_METHOD"] === "POST") {

  // Data are held in the `data` key of the POST request
  extract(
    array_map(
      'htmlspecialchars',
      json_decode($_POST["data"], true)
    )
  );

  // ... Your instructions goes here ...

  // Use an object to return data and encode it in literal json
  $response = (object) [
    "key" => $value,
    ...
  ];
  $json = json_encode($response);

  // Send data
  echo $json;
}
```
