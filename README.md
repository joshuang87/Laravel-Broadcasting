# Requirement
- Laravel 9x
- Vue 3
- [Pusher Account](https://pusher.com/)

# Laravel Broadcasting

Laravel Broadcasting is...

1.Create a Laravel project with the command below
```
composer create-project --prefer-dist laravel/laravel YOUR_PROJECT_NAME
```
```
composer require pusher/pusher-php-server
```
2.Create a Channels App at Pusher.com

![image](https://user-images.githubusercontent.com/46678886/209334354-f69f9d1b-d621-4834-a870-239cf06c8d35.png)

Get your app keys and enter in your project's .env file,edit the *BROADCAST_DRIVER* part, and it will look be like this:
```
BROADCAST_DRIVER=pusher

PUSHER_APP_ID=YOUR_APP_ID
PUSHER_APP_KEY=YOUR_APP_KEY
PUSHER_APP_SECRET=YOUR_APP_SECRE
PUSHER_HOST=
PUSHER_PORT=443
PUSHER_SCHEME=https
PUSHER_APP_CLUSTER=YOUR_APP_CLUSTER
```
3.Create a Event and your YOUR_EVENT_NAME.php will be generate at app/Events
```
php artisan make:event YOUR_EVENT_NAME
```
edit your YOUR_EVENT_NAME.php as image below

![image](https://user-images.githubusercontent.com/46678886/209336259-2c0268e3-317d-450e-b932-1187a320642c.png)

go to config/app.php and uncommon the BroadcastServiceProvider::class

![image](https://user-images.githubusercontent.com/46678886/209337040-d0401412-7134-4d07-a6bd-938a61aba62f.png)

```
npm install pusher-js laravel-echo --save
```
create 2 web page at resources\views

![image](https://user-images.githubusercontent.com/46678886/209338353-38c53ac9-7e07-44f0-a9c1-09cc04a17afc.png)

![image](https://user-images.githubusercontent.com/46678886/209343335-8103626a-2e7b-48de-b38a-f5a1a97a2190.png)

go to routes/web.php and define our route

![image](https://user-images.githubusercontent.com/46678886/209338780-35dd76c0-b770-4889-a19b-781d8d08f13b.png)

go to resources/js/bootstrap.js and uncommon some code and it will look be like this

![image](https://user-images.githubusercontent.com/46678886/209339669-8a1faf90-1baa-4ef9-801a-915e437285de.png)

and change it
```
window.Echo = new Echo({
    broadcaster: 'pusher',
    key: import.meta.env.VITE_PUSHER_APP_KEY,
    cluster: import.meta.env.VITE_PUSHER_APP_CLUSTER,
    forceTLS: true
});
```
```
composer require laravel/ui
```
```
php artisan ui vue
```
```
npm install
```
go to resources/js/app.js and add few lines of code
```
const app = createApp({
    created(){
        window.Echo.channel('YOUR_CHANNEL_NAME').listen('YOUR_EVENT_NAME',(e)=>{
            console.log('Sended')
        })
    }
});
```

go to routes/channels.php and add few lines of code
```
Broadcast::channel('YOUR_CHANNEL_NAME', function () {
    return true;
});
```
After that, go back to listen.blade.php to add a div with id call app
```
<body>
    <div id="app">
        <h1>This is Listen page</h1>
    </div>
</body>
```
start your project
```
php artisan serve
npm run dev
```


https://user-images.githubusercontent.com/46678886/209351694-73b86c54-4cd0-455d-a8be-8497e5cc64b1.mp4

