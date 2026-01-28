using System.Text.RegularExpressions;

string ein = Regex.Match(text, @"\b\d{2}-?\d{7}\b").Value;

string assetsRaw = Regex.Match(
    text,
    @"Total Assets\s+([\d,]+)"
).Groups[1].Value;

decimal totalAssets = 0;
decimal.TryParse(assetsRaw.Replace(",", ""), out totalAssets);









