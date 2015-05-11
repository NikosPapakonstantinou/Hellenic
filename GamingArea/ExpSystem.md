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
TeamXPFactor = TeamXP / N

If player drops ( exclude ), his XP aren't counted 

TeamXPFactor is calculated for both teams, so we can compare which team was stronger.

casebonus is counted for winning team only, and its 2*enemyspree if spree > 4

BaseTeamFactor = DefTeamFactor

Based on game length, we modify it a little bit
If Gamelength < 30 BTF = BTF/1.5
IF Gamelength < 45 BTF = BTF/1.3
else BTF = BTF

( ^^ this is where it comes to possible abuse, but few warns will do it :P => RESULT GAME ASAP )

;;;;;;;;;; TEAM FACTOR ;;;;;;;;;;;;

TeamFactor for winning team:

TeamFactor = BaseTeamFactor - (winnercount-losercount) * TeamCountModifier
TeamGain = RatingChange(TF,COMP(WinnerXP,LoserXP))

Where COMP(teamA,teamB) is
COMP = teamA/teamB
COMP = 1/COMP

Where RatingChange(FAC,MODIFIER) = FAC*MODIFIER

TeamGain = TeamGain + casebonus + randombonus

TeamFactor for losing team:

TeamFactor = BaseTeamFactor + (losercount-winnercount)*TeamCountModifier
TeamLoss = RatingChange(TF,COMP(WinnerXP,LoserXP))
TeamLoss = TeamLoss - RandomBonus/2


;;;;;;;;;; PLAYER FACTOR ;;;;;;;;;;;;

First, we get streak modifier:
3+ = 1.2
5+ = 1.4
7+ = 1.6
9+ = 1.8

Then we get base XP for this player based on #games he played ( 30,25,20,15 )

His new base is then base*streak modifier

For Winning team:
wonxp = RatingChange(BASE,COMP(PlayerXP,LoserXP))
wonxp = wonxp + TeamGain

For Losing team:
lostxp = RatingChange(BASE,COMP(WinnerXP,PlayerXP))
lostxp = lostxp + TeamLoss

;;;;;;;;;;;;;;;;; XP MODIFIERS ;;;;;;;;;;;;;;;;;;
if players XP are <800, he gets a special *1.3 bonus to wonXP and /1.3 
to lostXP and additional +0.1 for every 50xp dropped

if players XP are >1400 he gets a special /1.3 infliction to wonXP 
and *1.3 to lostXP and additional +0.1 for every 50xp gained
*/
