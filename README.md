# brat-documentation-extras
Some helpful tips I have learned while using the Brat annotation tool

DISCLAIMER: I am in no way an expert on brat, I simply want to share some of the things I have learned while working with Brat, trying to explain these things in a way that is hopefully easy to understand.

A lot of information about Brat is scattered, and some information is in the code itself. I want to describe some of the things that have been useful for me and for the project I am working on. Maybe I have just missed these things in the main documentation.

The main Brat manual is here:
https://brat.nlplab.org/manual.html


### Giving user permissions
User permission is supported, but not documented by Brat. The user-permissions are controlled by a configuration (.conf)  document called acl.conf, as with the visual, shortcut and annotation configuration files. 
In server/src/projectconfig.py the default acl.conf is described. It looks like this:
> User-agent: *                                                                   
> Allow: /                                                                        
> Disallow: /hidden/                                                              
>                                                                                 
> User-agent: guest                                                               
> Disallow: /confidential/

The first line means that the lines after apply to all users. User-agent are the usernames as they are defined in the dictionary USER_PASSWORD in the config.py-file. The slash (\/) refers to the current directory. 
The word "guest" seems to be a specific word referring to all those who access the site but are not logged in as users.
The default document therefore says: all users are allowed to access the current directory, but they are not allowed to access the /hidden/ directory. All guest users are not allowed to access the /confidential/ directory.

So if I have the users user1,user2 and user3, and I want to have three folders, one for each user, I can restrict access by having an acl.conf-file in each folder. An example for user1's folder would look like this:

> User-agent: *  
> Disallow: /  
>  
> User-agent: user1  
> Allow: /  

This means that in general I restrict access to everyone for the current directory, but after that I specify that user1 should have access.




Sources:  
https://github.com/nlplab/brat/blob/master/configurations/acl.conf  
https://github.com/nlplab/brat/issues/1002  

# Special options for config files


To specify events with optional arguments:

Role:Type    (exactly one)
Role?:Type   (zero or one)
Role+:Type   (one or more)
Role*:Type   (zero or more)

We should support also specifying a fixed number of arguments. As a use case, ACE MERGE-ORG events take exactly two Org arguments. As an obvious extension, it would be good to support argument number ranges.

Given the use of regex-like syntax for the argument specs, one obvious alternative for config syntax would be like

Role{2}:Type    (exactly two)
Role{2,4}:Type  (between two and four)


https://github.com/nlplab/brat/issues/434
