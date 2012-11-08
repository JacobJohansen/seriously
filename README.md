Looking for New Maintainer
--------------------------
I'm no longer doing iOS development, so I am not using seriously anymore. If
you would like to take over as maintainer of seriously let me know!


Seriously
---------
The iPhone needs a better way to make HTTP requests, specifically calls to 
REST web services. Seriously mixes Blocks with NSURLConnection & 
NSOperationQueue to do just that. It also will automatically parse the JSON 
response into a dictionary if the response headers are set correctly.

Install
-------
Just drag the files from the "src" directory into your project. You can also try
using the included "Seriously.framework" file

Parse JSON EXAMPLE
------------------
    NSString *url = @"http://api.twitter.com/1/users/show.json?screen_name=probablycorey"

    [Seriously get:url handler:^(id body, NSHTTPURLResponse *response, NSError *error) {
        if (error) {
            NSLog(@"Error: %@", error);
        }
        else {
            NSLog(@"Look, JSON is parsed into a dictionary!");
            NSLog(@"%@", [body objectForKey:@"profile_background_image_url"]);
        }
    }];

Simple Queue Example 
--------------------
    NSArray *urls = [NSArray arrayWithObjects:
                     @"http://farm5.static.flickr.com/4138/4744205956_1f08ae40e3_o.jpg",
                     @"http://farm5.static.flickr.com/4123/4744238252_d11d0df5a3_b.jpg",
                     @"http://farm5.static.flickr.com/4097/4743596319_50cce97d80_o.jpg",
                     @"http://farm5.static.flickr.com/4099/4743581287_7c50529b36_o.jpg",
                     @"http://farm5.static.flickr.com/4123/4743587437_78f0906e8a_o.jpg",
                     @"http://farm5.static.flickr.com/4136/4743562971_d5f5c6d5b1_o.jpg",
                     @"http://farm5.static.flickr.com/4073/4744205142_be44e64ab7_o.jpg",
                     nil];

    // By default the NSOperation will only do 3 requests at a time
    for (NSString *url in urls) {
        NSOperation *o = [Seriously request:url options:nil handler:^(id body,
        NSHTTPURLResponse *response, NSError *error) {            
            NSLog(@"got %d (%@)", [urls indexOfObject:url], url);
        }];
    }
 
Why Are You Using Blocks?
-------------------------
Welcome to the future dude!
 
TODO
----
- Document
- Add XML parsing
- Add more options for NSOperationQueue management
