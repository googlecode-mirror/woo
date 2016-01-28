# Woo Routing 1.0 #
Woo Routing is flexable routing system for php5.<br />
<b>Woo Routing feature:</b>
  * easy to add custom and dynamic routing url to route collection.
  * easy to create constraits which restrict URLs that match a paticure route.
  * supporting catchall style in the route match.
  * using route debugger to show routes match status in route collection when directly type  U
RL address in the browser address bar.
  * easy to create custom route handler to process the URL that match a paticular route in the route
collection.

<b>Route Rule:</b><br />
There have name,url, defaults, constraints,dataTokens,routeHandler in each route rule.<br />
<b>name:</b>    route name need be unqiue in the route collection <br />
<b>url: </b>        might be contain some tokens included in{ and } like {controller} which token name is controller <br />
<b>defaults:</b>  defaults define token name in url default values <br />
<b>constraint:</b> constraint restrict token value in the route, and support two style constraint, one is pattern match, another is php object which implement Routing\IRouteConstraint interface.<br /><br />
<b>A Practical approach:</b><br />
There is a function named function registe\_Route($routes) in the global.php file.<br />
There already have five demo routes in the route collection.<br />
```
/**
 * 
 * registe applicaton route rule
 * @param Woo\Routing\RouteCollection $routes
 */
function registe_Route($routes){	
	    /**
	     * 
	     * Routing\StopRouteHandler is demo RouteHandler which just print out $requestContext.
	     * Comment bellow statement  if use other RouteHandler which need implement Routing\IRouteHandler interface.
	     */
     	$routeHandler = new Routing\StopRouteHandler();
     	
        /**
         * map routes
         * just demo route rules
         * $routes->mapRoute($name, $url, $defaults, $constraints, $dataTokens,$routeHandler)
         */
     	
     	$routes->mapRoute(
     	 'BlogArchive', /*name*/
     	 'Archive/{date}', /*url*/
      	array('controller'=>'Blog','action'=>'Archive'), /*defaults*/
     	array('date'=>'\d{4}\-\d{2}\-\d{2}'),           /*constraints*/
     	array(),                                         /*dataTokens*/
     	$routeHandler                                    /*routeHandler*/
     	);   
     	         
        $routes->mapRoute(
     	 'Car', /*name*/
     	 'Car/{make}.{mode}', /*url*/
      	array('controller'=>'Car','action'=>'Index'), /*defaults*/
     	array('make'=>'(red|blue)',"httpget"=>new Routing\HttpMethodConstraint("get")),           /*constraints*/
     	array(),                                         /*dataTokens*/
     	$routeHandler                                    /*routeHandler*/
     	); 
     	 
     	$routes->mapRoute(
     	 'Admin', /*name*/
     	 'Admin/{controller}/{action}', /*url*/
      	array('controller'=>'Home','action'=>'Index'), /*defaults*/
     	array(),           /*constraints*/
     	array('area'=>'Admin','namespace'=>'Myapp\Admin'),/*dataTokens*/                                         /*dataTokens*/
     	$routeHandler                                    /*routeHandler*/
     	); 
     	
     	$routes->mapRoute(
     	 'Search', /*name*/
     	 'Search/{*q}', /*url catch all*/
      	array('controller'=>'Search','action'=>'Index'), /*defaults*/
     	array(),           /*constraints*/
     	array(),                                         /*dataTokens*/
     	$routeHandler                                    /*routeHandler*/
     	); 
     	
     	$routes->mapRoute(
     	 'Defaults', /*name*/
     	 '{controller}/{action}/{id}', /*url*/
      	array('controller'=>'Home','action'=>'Index','id'=>''), /*defaults*/
     	array(),           /*constraints*/
     	array(),                                         /*dataTokens*/
     	$routeHandler                                    /*routeHandler*/
     	); 

}
```




# What is Woo? #
Woo is fast and light-weight php web components for easy usage.
Woo components include url routing, mvc, orm, configuration, template engine etc.