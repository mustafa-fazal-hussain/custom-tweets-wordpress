# custom-tweets-wordpress
How to display custom layout of tweets in WordPress.

# place the above folder in yoyr theme folder 
like wp-content/themes/YOURTHEME/twitter-plugin/past folder

# write this function in your theme's function.php file

function showTweets($tweets_attr)
{
	
	require_once('twitter-plugin/TweetPHP.php');	
	
	extract(shortcode_atts(array(
			'consumer_key'       	  => '', //YOUR CONSUMER KEY
			'consumer_secret'    	  => '', //YOUR CONSUMER SECRET
			'access_token'          => '', //YOUR ACCESS TOKEN
			'access_token_secret'   => '', //YOUR ACCESS TOKEN SECRET
			'twitter_screen_name'   => '', //YOUR TWITTER NAME
			'tweets_to_display'     => 10, //  NUMBER OF TWEETS TO DISPLAY
			'cachetime'             => 60 * 60,
			'debug'    				=> false,
		
	), $tweets_attr));
	
			$output_tweets	 = '';
				$TweetPHP 		 = new TweetPHP(array(
											'consumer_key'          => $consumer_key,
											'consumer_secret'       => $consumer_secret,
											'access_token'          => $access_token,
											'access_token_secret'   => $access_token_secret,
											'twitter_screen_name'   => $twitter_screen_name,
											'tweets_to_display'    	=> $tweets_to_display,
											'cachetime'            	=> $cachetime,
											'debug'    				=> $debug,
										));
                    
	$output_tweets	    .= 	'<div class="myclassname">'.$TweetPHP->get_tweet_list().'</div>';
  
	return $output_tweets;
}
add_shortcode('show-custom-tweets', 'showTweets');


# call tweets by this method

  [show-custom-tweets]

