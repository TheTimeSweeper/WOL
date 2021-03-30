# WOL Mods
Mods for the fabulous game Wizard Of Legend

-----Hera are an instruction on how to add your own cloaks-----

Install dnSpy, or any other decompiler of your choice.
Open the game files, edit the List<Outfit> OutfitList in the Outfit class, now you edit or add a cloak according to the following structure:

list.Add(new Outfit(String anyName, int anyPaletteIndex, new List<OutfitModStat>
{
new OutfitModStat(OutfitModStat.OutfitModType.(Any), 0f, 0f, 0f, false),
}, false, false));

anyName is the name as refered to in the game files and will, when an actual name is added, not be visible in-game

anyPaletteIndex is technically not too open with the possible values (I think it's around 20-isch)

(any) is of course just the name of the outfitmodtype, and those could for example be Health, Armor and Evade, you could of course have more than one outfitmodtype on a single cloak.

The three float values which comes after are to specify how much it affect it, and they could have different positions depending on the outfitmodtype you choose, an "Evade, 1f, 0f, 0f, false" will give perfect (100%) evasion

next we will go to the TextManager class and look for the LoadOutfitJSON() method and change it so it looks like this

private static void LoadOutfitJSON()
{
TextManager.outfitInfoDict = new Dictionary<string, string>();
TextManager.UITextContainer uitextContainer = JsonUtility.FromJson<TextManager.UITextContainer>(ChaosBundle.Get<TextAsset>(TextManager.outfitInfoPath).text);
int num = uitextContainer.uiTexts.Length;
for (int i = 0; i < num; i++)
{
TextManager.UITextInfo uitextInfo = uitextContainer.uiTexts[i];
TextManager.outfitInfoDict[uitextInfo.uiTextID] = uitextInfo.displayText;
}
TextManager.outfitInfoDict[anyName] = String realDisplayName;
} 

anyName is the name from before and the realDisplayName is the name you want it to have ingame
