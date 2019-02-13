# Ms. Marple's Jam Emporium

Our largest client Ms. Marple, runs the 17th largest online Jam Emporium in Staines-upon-Thames.  To help her reach all of her devoted customers, we're in the process of swapping out her monolithic Drupal backend with a spangly new one.

The developer in charge of the API part of this project has provided the following documentation along with an executable file (`qa_api_mac` for Mac users, `qa_api_lin` for Linux users and `qa_api_win.exe` for Windows users) which runs a service on port 8080.  Before we give it the go ahead for a production release to Ms. Marple's website, we'd like you to put it through its paces and come back to us with your findings.  Sorry to have to chuck it over the dev/test fence!

## A note on the files

### Running on Macs and Linux

Once downloaded, you'll want to run the application from the terminal.  The file won't have execute permissions by default, so run the following to open the application:

``` bash
$ chmod +x <FILE_NAME>

$ ./<FILE_NAME>
```

### Integrity

If you'd like to check the integrity of the files you download, here are the SHA256 digests:

``` bash
19f4fd7c7cfa2b033e89456df6437770a9c8a30409e8bb193235e0a83c189213  qa_api_mac
f0be5c4d1bd8d3eb9a79692749f43a84f040736bef43778cfc0733358cb1764a  qa_api_lin
c64a035157bae437a197c4e4e20e14997859136eeb4387d5d961cd484b1ef676  qa_api_win.exe
```

## Users

The service has been configured with 3 users, it's not currently possible to create new users but you'll be able to test with one of these:

| Username | Password |
|-|-|
| alice | a37d3106168770fa4477903703c548c7010ea570  |
| bob | b3600ebd0b0b88e0ecfcb467e3fd93865d835aee  |
| carol | c1702bcfa2205d82e2c95a6f1c502627d3562453 |

## Endpoints

### /login POST
Log into the service as a given user.  For example:

``` json
{
	"username": "alice",
	"password": "a37d3106168770fa4477903703c548c7010ea570"
}
```

### /products GET
Lists all products.

* This endpoint is rate-limited to prevent too many requests being made at once.  With a bit of profiling, we found that 50 requests/s with bursts of up to 100 requests/s for the busy morning Jam rush was about right.

### /products/{id} GET
Finds a product by its id.

### /products POST
Creates a new product.  For example:

``` json
{
	"name": "Lime Curd",
	"available": 100
}
```

* Product names have a maximum length of 100 characters.

### /products/{id} PUT
Updates a product by its id.

``` json
{
	"id": 4,
	"name": "Lime Curd",
	"available": 150
}
```

### /products/{id} DELETE
Deletes a product by its id.

### /products/{id} POST
Buys an item for the currently logged in user.  For example:

``` json
{
	"user_id": 1,
	"amount": 5
}
```

## Extra

* Data is not persisted anywhere, so if you need to reset things, just restart the server.