# Exploring Game Reccommendation Ideas
Video Game Recommendation Engine

### Repo to explore Video Game Recommendation ideas and approaches



# Data Description
Steam IDs are unique, 64-bit values representing a specific Steam user.

## Data Source
CONDENSING STEAM: DISTILLING THE DIVERSITY OF GAMER BEHAVIOR
https://steam.internet.byu.edu/oneill-condensing-steam.pdf

## Data downloaded
https://steam.internet.byu.edu


### ACHIEVEMENT_PERCENTAGES
This table was obtained through the Web API [ISteamUserStats::GetGlobalAchievementPercentagesForApp]. It contains achievmeent completion data for all the products listed in the App_ID_Info table.

* appid - The ID of the game in question
* Name - The name of the achievement as it appears to players. As an internal value assigned by developers, its descriptiveness of the achievement varies.
* Percentage - The percentage of players who have finished this achievement out of all total players who own this game.


### APP_ID_INFO
This table was derived from scanning the steam storefront by emulating the REST API calls issued by the Steam client's "Big Picture mode". It contains selected information for each product ("app") offered on Steam. An older version of this table from the time of our first data pull can be found with an "_Old" suffix.

* appid - The ID of the "app" in question, which is not necessarily a game.
* Title -  The Title of the app, as it appears to users
* Type - The type of the "app". Possible values include: "demo," "dlc," "game," "hardware," "mod," and "video." Game is the most common.
* Price - The current price of the "app" on the Steam storefront, in US dollars. Free items have a price of 0.
* Release_Date - The date the "app" was made available via the Steam storefront. Note that apps released elsewhere originally and later published through steam carry the date of the Steam publish
* Rating - The rating of the "app" on Metacritic. Set to -1 if not applicable.
* Required_Age - The MSRB or PEGI-assigned age requirement for viewing this game in the Steam storefront, and, by extension, clicking the button to purchase it.
* Is_Multiplayer - A value of either 0 or 1 indicating whether or not an "app" contains multiplayer content. Self-reported by developers.


### FRIENDS
This table was obtained through the Web API [ISteamUser::GetFriendList]. It contains a list of the (reciprocal) friendships of steam users.

* steamid_a - The Steam ID of the user who's friend list was queried
* steamid_b - The Steam ID of the a user who is a friend of the user referenced by steamid_a
* relationship -  The type of relationship represented by this entry. Currently the only value used is "friend"
* friend_since -  The date and time when the users in this entry became friends. Note that this field was added in 2009 and thus all frienships existing previous this date are recorded with the default unix timestamp (1970)
* dateretrieved -  Timestamp when this friend list data was requested from the API


### GAMES_1
This table was obtained through the Web API [IPlayerService::GetOwnedGames]. It contains the game data requested during our initial crawl of the Steam network.
* steamid - The steam ID of the user in question
* appid - The ID of a given app in the user's library
* playtime_2weeks - The total time the user has run this app in the two-week period leading up to when this data was requested from the API. Values are given in minutes.
* playtime_forever - The total time the user has run this app since adding it to their library. Values are given in minutes.
* dateretrieved - Timestamp of the time when this game data was requested from the API


### GAMES_2
This table was obtained through the Web API [IPlayerService::GetOwnedGames]. It contains the game data requested during our follow-up crawl of the Steam network.

* steamid - The steam ID of the user in question
* appid - The ID of a given app in the user's library
* playtime_2weeks - The total time the user has run this app in the two-week period leading up to when this data was requested from the API. Values are given in minutes.
* playtime_forever - The total time the user has run this app since adding it to their library. Values are given in minutes.
* dateretrieved - Timestamp of the time when this game data was requested from the API

### GAMES_DAILY
This table was obtained through the Web API [IPlayerService::GetOwnedGames]. It contains the game playing data for a select subset of users. Each user's data in the subset was requested repeatedly, every day for five days.

* steamid - The steam ID of the user in question
* appid - The ID of a given app in the user's library
* playtime_2weeks - The total time the user has run this app in the two-week period leading up to when this data was requested from the API. Values are given in minutes.
* playtime_forever - The total time the user has run this app since adding it to their library. Values are given in minutes.
* dateretrieved - Timestamp of the time when this game data was requested from the API


### GAMES_DEVELOPERS
This table was derived from scanning the steam storefront by emulating the REST API calls issued by the Steam client's "Big Picture mode". It contains the names of the developers for each product on Steam. This is a sister table to App_ID_Info. An older version of this table from the time of our first data pull can be found with an "_Old" suffix.

* appid - ID of the app in question
* Developer - A developer of the app in question. Note that some apps have multiple developers and thus numerous distinct rows with the same appid are possible.

### GAMES_GENRES
This table was derived from scanning the steam storefront by emulating the REST API calls issued by the Steam client's "Big Picture mode". It contains the names of the genres for each product on Steam. This is a sister table to App_ID_Info. An older version of this table from the time of our first data pull can be found with an "_Old" suffix.

* appid - ID of the app in question
* Genre - A genre of the app in question. Note that most apps have multiple genres and thus numerous distinct rows with the same appid are possible.

### GAMES_PUBLISHERS
This table was derived from scanning the steam storefront by emulating the REST API calls issued by the Steam client's "Big Picture mode". It contains the names of the publishers for each product on Steam. This is a sister table to App_ID_Info. An older version of this table from the time of our first data pull can be found with an "_Old" suffix.

* appid - ID of the app in question
* Publisher - A publisher of the app in question. Note that some apps have multiple publishers and thus numerous distinct rows with the same appid are possible.

### GROUPS
This table was derived from the steamcommunity.com XML data. It contains a list of all the group memberships of each user.

* steamid - The developer of the app in question
* groupid - A group ID for a group to which te user referenced by steamid belongs. Users may belong to more than one group.
* dateretrieved - Timestamp of the time when this game data was requested from the API

### PLAYER_SUMMARIES
This table obtained through the Web API [ISteamUser::GetPlayerSummaries]. It contains a profile summary for each Steam user.

* steamid - The Steam ID of the user in question
* lastlogoff - Timestamp of the time when this game data was requested from the API
* primaryclanid - The groupid (Groups::groupid) of the group that the user has designated as their primary group
* timecreated - Timestamp of the time when the account was created
* gameid - If the user was in-game at the time of the API request, this value specifies which game they were running at the time
* gameserverip - If the user was in-game at the time of the request, and playing a game using Steam matchmaking, this value specifies the IP of the server they were connected to. Is otherwise set to "0.0.0.0:0"
* loccountrycode - ISO-3166 code for the country in which the user resides. Self-reported.
* locstatecode - State where the user resides. Self-reported.
* loccityid - Internal Steam ID corresponding to the city where the user resides. Self-reported.
* dateretrieved - Timestamp of the time when this game data was requested from the API

