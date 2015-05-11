/*
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
EXP SYSTEM
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

team-xp factor - Same for whole team, for winning with excluded players and so.

user-xp factor - Unique for every player, low xp, rank etc

casebonus - spree ending, random bonus etc

There are 4 levels of Base XP for game
Newbie games ( <40 ) = 30
Experienced games ( <100 ) = 25
Veteran games ( <400 ) = 20
above Veteran = 15

DefaultTeamFactor = 18
TeamCountModifier = 10 ( for team count difference, when some1 is excluded )
randombonus = 2*R(1,4) (2k4)

First, teamXP factor is calculated:

TeamXP = player1...playerN XP 
