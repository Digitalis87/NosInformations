```
#=======
BEGIN
VNUM	{QueteID}	{QueteType}	1	1	-1	-1
LEVEL	{NiveauMin}	{NiveauMax}
TITLE	{TitreQuete}
DESC	{InfoQuete}
TALK	{IDDialogue}  {?}	{NPCVNum(?)}	{IDDialogueFin}
TARGET	{MapID} {MapX}	{MapY}
DATA	{Data1} {Data2} {Data3} {Data4} 
PRIZE	{TypeRecompense}	{Data}	{Quantité}  {IDQuete}
LINK	{QueteSuivante}
END
#=======
```

---

Infos **QueteType** : La ligne **DATA** change selon le type de quete
```cs
case QuestType.Hunt: 1 
case QuestType.Capture1: 2
case QuestType.Capture2: 5
case QuestType.Collect1: 6 
case QuestType.Product: 8
                                        data = int.Parse(currentLine[1]);
                                        objective = int.Parse(currentLine[2]);
```                                        
```
DATA {Data1} {Objectif}
```
---
```cs
case QuestType.Brings: 4
DATA  {npcVNum}  {QuantitéRequise}  {ItemVNum} 

case QuestType.Collect3: 13
DATA  {ItemVNum}  {ItemObjectif}  {TimestoneID}

case QuestType.Needed: 16
DATA  {ItemVNum}  {Objective} {NpcVNum}

case QuestType.Collect5: 20 // Collecter des entités de carte = Fleur de glace, blé, eau, etc
DATA  {ItemVNum}  {Objective} {npcVNum}

                                        specialData = int.Parse(currentLine[1]);
                                        data = int.Parse(currentLine[2]);
                                        objective = int.Parse(currentLine[3]);
                                        
```
---
```cs
case QuestType.Collect4: 17 
DATA  {ItemVNum}  {Objective} {MonsterVNum} {DropRate} 
case QuestType.Collect2: 3 
DATA  {ItemVNum}  {Objective} {MonsterVNum} {DropRate} 
                                        specialData = int.Parse(currentLine[1]);                                      
                                        data = int.Parse(currentLine[2]);
                                        objective = int.Parse(currentLine[3]);
                                        secondSpecialData = int.Parse(currentLine[4]);
```
---
```cs
case QuestType.TimesSpace: 7
DATA {TSLvl}  {Objective} {TS Id} //JE SAIS PAS DANS QUEL SENS SONT LES DATA/OBJECTIVE/SPECIALDATA //
case QuestType.TsPoint: 11
                                        data = int.Parse(currentLine[4]);
                                        objective = int.Parse(currentLine[2]);
                                        specialData = int.Parse(currentLine[1]);
```
---
```cs
case QuestType.Wear: // Item VNum - * - NpcVNum //
                                        data = int.Parse(currentLine[2]);
                                        specialData = int.Parse(currentLine[1]);
                                        break;

                                    case QuestType.TransmitGold: // NpcVNum - Gold x10K - * //
                                        data = int.Parse(currentLine[1]);
                                        objective = int.Parse(currentLine[2]) * 10000;
                                        break;

                                    case QuestType.GoTo: // Map - PosX - PosY //
                                        data = int.Parse(currentLine[1]);
                                        objective = int.Parse(currentLine[2]);
                                        specialData = int.Parse(currentLine[3]);
                                        break;

                                    case QuestType.WinRaid: // Design - Objective - ? //
                                        data = int.Parse(currentLine[1]);
                                        objective = int.Parse(currentLine[2]);
                                        specialData = int.Parse(currentLine[3]);
                                        break;

                                    case QuestType.Use: // Item to use - * - mateVnum //
                                        data = int.Parse(currentLine[1]);
                                        specialData = int.Parse(currentLine[2]);
                                        break;

                                    case QuestType.Dialog1: // npcVNum - * - * //
                                    case QuestType.Dialog2: // npcVNum - * - * //
                                        data = int.Parse(currentLine[1]);
                                        break;

                                    case QuestType.FlowerQuest:
                                        objective = 10;
                                        break;

                                    case QuestType.Inspect: // NpcVNum - Objective - ItemVNum //
                                    case QuestType.Required: // npcVNum - Objective - ItemVNum //
                                        data = int.Parse(currentLine[1]);
                                        objective = int.Parse(currentLine[3]);
                                        specialData = int.Parse(currentLine[2]);
                                        break;

                                    default:
                                        data = int.Parse(currentLine[1]);
                                        objective = int.Parse(currentLine[2]);
                                        specialData = int.Parse(currentLine[3]);
                                        break;
                                }

                                currentObjectives.Add(new QuestObjectiveDTO
                                {
                                    Data = data,
                                    Objective = objective,
                                    SpecialData = (specialData < 0 ? 0 : specialData),
                                    DropRate = (secondSpecialData < 0 ? 0 : specialData),
                                    ObjectiveIndex = objectiveIndex,
                                    QuestId = (int)quest.QuestId
                                });
                                break;
