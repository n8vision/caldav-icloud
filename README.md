#Ruby CalDAV library for iCloud Caldav

[![Join the chat at https://gitter.im/n8vision/caldav-icloud](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/n8vision/caldav-icloud?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
**caldav-icloud is based on agilastic/agcaldav, modified to work for Apple's iCloud**

**caldav-icloud is still under development and is not finished...**

##Usage Events

First, you've to install the gem

    gem install caldav-icloud

and require it

    require "caldav-icloud"

Now you can e.g. create a new CalDAViCloud-Client:
    	
	cal = CalDAViCloud::Client.new(:uri => "https://pYY-caldav.icloud.com/XXXXXXXXX/calendars/ZZZZZZZZ-ZZZZ-ZZZZ-ZZZZ-ZZZZZZZZZZZZ/", :user => "icloudusername@email.com" , :password => "icloudpassword")

Where X, Y, and Z (corresponding to your closest icloud caldav server, icloud unique id, and calendar uuid path respectively) can be found with these links: 

https://www.google.com/search?client=safari&rls=en&q=finding+your+icloud+user+id&ie=UTF-8&oe=UTF-8#q=finding+your+icloud+unique+id+caldav+path&rls=en

http://apple.stackexchange.com/questions/67021/how-can-i-configure-custom-repeat-intervals-for-reminders

####Find Events within time interval

    result = cal.find_events(:start => "2012-10-01 08:00", :end => "2013-01-01")

    >> result
    => [#<Icalendar::Event:0x007f8ad11cfdf0 @name="VEVENT", @components={}, @properties={"sequence"=>0, "dtstamp"=>#<DateTime: 2012-12-31T13:44:10+00:00 (4244474429/1728,0/1,2299161)>, "description"=>"sdkvjsdf sdkf sdkfj sdkf dsfj", "dtend"=>#<DateTime: 2012-12-30T12:00:00+00:00 (2456292/1,0/1,2299161)>, "dtstart"=>#<DateTime: 2012-12-29T10:00:00+00:00 (29475491/12,0/1,2299161)>, "summary"=>"12345", "uid"=>"b2c45e20-3575-0130-7d2e-109add70606c", "x-radicale_name"=>"b2c45e20-3575-0130-7d2e-109add70606c.ics"}>, #<Icalendar::Event:0x007f8ad10d7dd0 @name="VEVENT", @components={}, @properties={"sequence"=>0, "dtstamp"=>#<DateTime: 2012-12-31T13:44:10+00:00 (4244474429/1728,0/1,2299161)>, "uid"=>"b2c45e20-3575-0130-7d2e-109add70606c", "x-radicale_name"=>"b2c45e20-3575-0130-7d2e-109add70606c.ics"}>]

    >> result.class
    => Array

    >> result.count
    => 2

####Create an Event

    result = cal.create_event(:start => "2012-12-29 10:00", :end => "2012-12-30 12:00", :title => "12345", :description => "12345 12345")

Analyze result:
   
    >> result
    => #<Icalendar::Event:0x007ff653b47520 @name="VEVENT", @components={}, @properties={"sequence"=>0, "dtstamp"=>#<DateTime: 2012-12-30T19:59:04+00:00 (26527957193/10800,0/1,2299161)>, "description"=>"sdkvjsdf sdkf sdkfj sdkf dsfj", "dtend"=>#<DateTime: 2012-12-30T12:00:00+00:00 (2456292/1,0/1,2299161)>, "dtstart"=>#<DateTime: 2012-12-29T10:00:00+00:00 (29475491/12,0/1,2299161)>, "summary"=>"12345", "uid"=>"e795c480-34e0-0130-7d1d-109add70606c", "x-radicale_name"=>"e795c480-34e0-0130-7d1d-109add70606c.ics"}> 
   
    >> result.class
    => Icalendar::Event

   
get UID of this Event:

    >> result.uid
    => "e795c480-34e0-0130-7d1d-109add70606c"


####Find an Event  (via UUID)  

    result = cal.find_event("e795c480-34e0-0130-7d1d-109add70606c")
    
    >> result.class
    => Icalendar::Event




####Delete Event

    cal.delete_event("e795c480-34e0-0130-7d1d-109add70606c")


####Update Event

**Not tested**

    event = {:start => "2012-12-29 10:00", :end => "2012-12-30 12:00", :title => "12345", :description => "sdkvjsdf sdkf sdkfj sdkf dsfj"}
    # set UUID 
    event[:uid] => "e795c480-34e0-0130-7d1d-109add70606c"
    c = cal.update_event(event)



##Usage ToDo

Not tested yet

##Work to be done ...

1. find and notify if overlapping events              
2. code cleanup -> more ActiveRecord style    
            
                                                             

##Contributors

[Check all contributors][c]


1. Fork it.
2. Create a branch (`git checkout -b my_feature_branch`)
3. Commit your changes (`git commit -am "bugfixed abc..."`)
4. Push to the branch (`git push origin my_feature_branch`)
5. Open a [Pull Request][1]
6. Enjoy a refreshing Club Mate and wait

[c]: https://github.com/n8vision/caldav-icloud/contributors
[1]: https://github.com/n8vision/caldav-icloud/pulls/

