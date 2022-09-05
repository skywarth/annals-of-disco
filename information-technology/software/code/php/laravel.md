## Events

There are events and observers/listeners. Listeners subscribe to event(s) and do actions. Events fire when certain things happen, you fire it explicitly. 

Events and listeners registered in `EventServiceProvider`.

### Generating event and listener fiels

`php artisan event:generate` looks up into the `EventServiceProvider`, creates events and listeners classes accordingly. But this one does the folder structure uglier. So i don't recommend it. It stores both the event and the listener in providers folder 🤢

Or you may use:

`php artisan make:event PodcastProcessed` and `php artisan make:listener SendPodcastNotification --event=PodcastProcessed`. Remember to register these into the `EventServiceProvider` !

You are not obliged to create listener classes, you can register them anonymously into the `boot()` function of an event.

### Events
- You can add as many properties as you want. Then you can indicate these dependencies and parameters in constructor.

### Listeners
- Listeners receive event instances in the handle method `public function handle(OrderShipped $event)`. But you don't have to explicitly indicate type, you may just apply loose-type. `public function handle($event)`
- You may type-hint any necessary dependency and service in handle parameters to inject it through service container

### Queuing
- Useful when you are going to perform time-consuming tasks in the **Listener**.
- Configure your queue in queue.php and start queue workers by either `queue:work` or `queue:listen`. (Don't forget to indicate the queue in work/listen !)
- If a listener is going to run on queue, implement `shouldQueue` interface on the listener clas.


### Misc

#### Queueable anonymous listener
you may use:
```
Event::listen(queueable(function (PodcastProcessed $event) {
        //
    }))->onConnection('redis')->onQueue('podcasts')->delay(now()->addSeconds(10)))
    ->catch(function (PodcastProcessed $event, Throwable $e) {
    // The queued listener failed...
}));
```
In a boot method of an event to register an anonymous (has no listener file) that runs using `queue` driver.

#### Wildcard event listener (anonymous)
```
Event::listen('event.*', function ($eventName, array $data) {
    //
});
```

#### Auto-discovery
I don't think it is a good future, can cripple performance a bit. Don't be a lazy-ass and define your events/listeners !

#### Production
Use `event:cache` on production to speed things up a bit. Clear 'em when you don't need 'em `event:clear`


#### Stop Event propagation
- **[!]** If you return false from handle method of a listener, it will stop propagation of the event.








### Cool packages

#### Health/Status
- https://github.com/antonioribeiro/health
- https://github.com/spatie/laravel-health

#### Error
- Flare


#### CI/CD
- https://www.laravel-enlightn.com/ (Performance and Security Insight)
