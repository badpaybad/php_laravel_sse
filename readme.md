# In your laravel project

Simple SSE implement with laravel
Pull git and copy keep structure files and folders

# Require

- REDIS server, work as queue
- Html5 support
- SharedWorker browser support
- Laravel or composer use auto loader with Dotenv\Parser
- .env
				REDIS_HOST=127.0.0.1
				REDIS_PORT=6379
				REDIS_DB=0
				REDIS_NOTI_DB=15


# Here description in diagram and code usage

https://docs.google.com/drawings/d/1DvaYDm2OtOsw7py2K1JDAOB4aKPhH5lan_KnT8_L7MY/edit?usp=sharing

# Javascript in your web

				const swUrl = '{{ asset("js/webpushnotification/notificationwebworker.js") }}?c=' + encodeURIComponent('CoWebNotification:UserOnline:<?php echo \Auth::user()->tenant_id ."_". \Auth::user()->id ?>')
					+'&s='+encodeURIComponent('co{{\Auth::user()->id}}');

				  var myWorker = new SharedWorker (swUrl);    
					    myWorker.port.onmessage=function(e){
						//todo: do smth with your: e.data
					    };
					    myWorker.port.start();

# php code to push data to web browser

$this->sse = new EventListenerHelper(env('REDIS_HOST'), env('REDIS_PORT'), env('REDIS_PASSWORD'), env('REDIS_NOTI_DB'));  
 $this->sse->SendNotifyToUser($user->tenant_id,$user->id,json_encode(
            array("datas"=>
                json_encode(array("title"=>"ping at ". Carbon::now(), "body"=>"Hello ".$user->username))    )    ));
