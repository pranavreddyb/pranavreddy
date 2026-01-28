string ein = Regex.Match(
    text,
    @"\b(EIN|Employer\s+Identification\s+Number)\b[:\s\-]*([\d\s\-]{9,})",
    RegexOptions.IgnoreCase
).Groups[2].Value
 .Replace(" ", "")
 .Replace("-", "");













