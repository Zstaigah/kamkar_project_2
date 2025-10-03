# OSINT Profile Generator CLI

![Version](https://img.shields.io/badge/version-1.0-blue.svg)
![Python](https://img.shields.io/badge/python-3.7+-green.svg)
![License](https://img.shields.io/badge/license-Educational-orange.svg)

An educational tool for cybersecurity training that generates realistic synthetic profiles with password hashes for OSINT practice, password security training, and penetration testing education.

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Usage](#usage)
- [Export Formats](#export-formats)
- [Hashcat Integration](#hashcat-integration)
- [Use Cases](#use-cases)
- [Technical Details](#technical-details)
- [Ethical Guidelines](#ethical-guidelines)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## Features

### Profile Generation
- Generate 1-1000 synthetic profiles with realistic data
- Personal information (name, age, contact, location)
- Professional details (job title, company, education)
- Social media profiles (LinkedIn, Twitter, GitHub)
- Password hints and hashes (SHA-512 standard or salted)

### Company Profiles
- Realistic company data with employee assignments
- Industry classifications and size ranges
- Department structures
- Website URLs and locations

### Export Capabilities
- **JSON** - Complete structured data
- **CSV** - Spreadsheet-compatible format
- **TXT** - Human-readable format
- **Hashes** - Various hashcat-compatible formats
- **HTML** - Interactive web visualizer
- **Wordlists** - Custom password lists

### Security Training Features
- Standard SHA-512 hashes (Mode 1700)
- Salted SHA-512 hashes (Mode 1710)
- Custom wordlist generation from profile data
- Hash reference files for validation
- Educational documentation

## Installation

### Requirements
- Python 3.7 or higher
- No external dependencies (uses Python standard library only)

### Setup

```bash
# Clone the repository
git clone https://github.com/yourusername/osint-profile-generator.git
cd osint-profile-generator

# Make executable (Linux/Mac)
chmod +x osint_cli_generator.py

# Run the tool
python3 osint_cli_generator.py
```

## Quick Start

### Basic Usage

```bash
# Launch the tool
python3 osint_cli_generator.py

# Follow the interactive menu:
# 1. Generate Profiles → Select amount → Choose hash type
# 2. Export Data → Choose format
# 3. Generate Wordlist → For password cracking practice
```

### Example Session

```python
# Generate 50 profiles with salted hashes
> 1  # Generate Profiles
> 3  # Medium Dataset (50 profiles)
> 2  # Several Companies (5)
> 2  # Salted SHA-512

# Export for hashcat
> 2  # Export Data
> 6  # Salted Hashcat Format
> training_hashes  # Custom filename

# Generate wordlist
> 4  # Generate Wordlist
> 1  # From current profiles
```

## Usage

### Menu Options

#### 1. Generate Profiles

Create synthetic profile datasets with customizable parameters.

**Profile Amounts:**
- Quick Test: 10 profiles
- Small Dataset: 25 profiles
- Medium Dataset: 50 profiles
- Large Dataset: 100 profiles
- Custom: 1-1000 profiles

**Company Amounts:**
- Few: 3 companies
- Several: 5 companies
- Many: 10 companies
- Custom: 1-20 companies

**Hash Types:**
- Standard SHA-512 (faster cracking, educational)
- Salted SHA-512 (realistic security training)

#### 2. Export Data

Export in multiple formats:

| Format | Description | Use Case |
|--------|-------------|----------|
| JSON | Complete structured data | Data analysis, archival |
| TXT | Human-readable format | Documentation, reporting |
| CSV | Spreadsheet format | Data analysis, Excel |
| Hashes (username:hash) | With usernames | Basic cracking |
| Hashcat Format | Clean hashes only | Direct hashcat use |
| Salted Hashcat | hash:salt pairs | Advanced training |
| Hash Reference | With password hints | Validation, learning |
| Salt Reference | Complete salted data | Understanding salts |

#### 3. Generate HTML Visualizer

Creates an interactive web interface with:
- Tabbed navigation (Profiles, Companies, Social Media)
- Real-time search functionality
- Statistics dashboard
- Responsive design
- No server required

#### 4. Generate Wordlist

Create custom password wordlists based on profile data.

**Pattern Types:**
- Base words (names, cities, companies)
- Name + year combinations
- Name + common numbers
- Two-word combinations
- Special character variations

**Example output:**
```
james
James1985
jamessmith
techcorp123
stanford99
```

#### 5. View Statistics

Display analytical information:
- Total profiles and companies
- Average age
- Most popular company
- Sample profile preview

#### 6. Clear All Data

Reset the generator (with confirmation prompt).

#### 7. Exit

Close the application.

## Export Formats

### JSON Structure

```json
{
  "metadata": {
    "exported_at": "2025-09-29T10:30:00",
    "total_profiles": 50,
    "total_companies": 5,
    "format": "OSINT_CLI_Export_v1.0"
  },
  "data": {
    "profiles": [
      {
        "id": "ID-1727601234-a1b2c3d4",
        "first_name": "James",
        "last_name": "Smith",
        "full_name": "James Smith",
        "email": "james.smith@techcorp.com",
        "phone": "+1-555-123-4567",
        "birthdate": "5/15/1985",
        "age": 40,
        "job_title": "Software Engineer",
        "company": "TechCorp Solutions",
        "city": "San Francisco",
        "university": "Stanford University",
        "linkedin_connections": 342,
        "password_hint": "James198545",
        "password_hash": "a665a4592042...",
        "salt": "3f2a8b9c1d4e5f6a...",
        "hash_type": "SHA-512_SALTED"
      }
    ]
  }
}
```

### CSV Columns

The CSV export includes 25+ columns:
- Personal: ID, FullName, FirstName, LastName, Age, Birthdate
- Contact: Email, Phone, City
- Professional: Company, JobTitle, University, GraduationYear
- Social: LinkedIn, Twitter, GitHub, LinkedInConnections
- Social Metrics: Posts, Followers, Following, LastActive
- Security: PasswordHint, PasswordHash
- Metadata: ProfileURL, GeneratedAt

## Hashcat Integration

### Hash Modes

**Standard SHA-512 (Mode 1700):**
```bash
hashcat -m 1700 -a 0 hashes.txt wordlist.txt
```

**Salted SHA-512 (Mode 1710):**
```bash
hashcat -m 1710 -a 0 salted_hashes.txt wordlist.txt
```

### Complete Workflow

```bash
# 1. Generate profiles with salted hashes
python3 osint_cli_generator.py
# Select: 1 → 50 profiles → 5 companies → Salted SHA-512

# 2. Export salted hashes
# Select: 2 → 6 (Salted Hashcat Format)
# Output: hashcat_salted_20250929_103000.txt

# 3. Generate wordlist
# Select: 4 → 1 (From current profiles)
# Output: osint_wordlist_20250929_103100.txt

# 4. Crack with hashcat
hashcat -m 1710 -a 0 -o cracked.txt \
  hashcat_salted_20250929_103000.txt \
  osint_wordlist_20250929_103100.txt

# 5. View results
hashcat -m 1710 --show hashcat_salted_20250929_103000.txt
```

### Hashcat Tips

**Optimize performance:**
```bash
# High workload
hashcat -m 1710 -a 0 -w 3 hashes.txt wordlist.txt

# Use rules
hashcat -m 1710 -a 0 -r rules/best64.rule hashes.txt wordlist.txt

# Session management
hashcat --session=training hashes.txt wordlist.txt
hashcat --session=training --restore
```

**Clear cached results:**
```bash
rm ~/.local/share/hashcat/hashcat.potfile
```

## Use Cases

### 1. Password Security Training

Demonstrate how personal information leads to weak passwords.

**Workflow:**
1. Generate 100 profiles with standard SHA-512
2. Export hashes and generate wordlist
3. Crack hashes with hashcat
4. Analyze success rates

**Learning Outcomes:**
- Personal data creates predictable passwords
- Social engineering attack vectors
- Importance of password complexity

### 2. OSINT Methodology Development

Practice data correlation and profile building.

**Workflow:**
1. Generate 500 profiles with HTML visualizer
2. Use search to find connections
3. Map relationships between profiles
4. Practice social network analysis

### 3. Penetration Testing Practice

Simulate credential attacks in a safe environment.

**Workflow:**
1. Generate enterprise dataset (200+ profiles)
2. Export salted hashes
3. Practice attack methodologies
4. Document findings and success rates

### 4. Security Awareness Training

Educate users about password security.

**Workflow:**
1. Generate profiles matching demographics
2. Show how quickly weak passwords crack
3. Demonstrate password policy importance
4. Build security culture

### 5. Academic Research

Study password patterns and human behavior.

**Workflow:**
1. Generate large datasets (500-1000 profiles)
2. Export to CSV for analysis
3. Analyze password pattern distributions
4. Compare with ethical breach research

## Technical Details

### Password Generation Algorithm

```python
def generate_password(profile):
    components = [
        profile['first_name'],        # "James"
        profile['last_name'],          # "Smith"
        str(profile['birth_year']),    # "1985"
        profile['city'],               # "Boston"
        profile['company'].split()[0]  # "TechCorp"
    ]
    
    # Combine two random components + 2-digit number
    return random.choice(components) + \
           random.choice(components) + \
           str(random.randint(10, 99))
```

### Hash Generation

**Standard SHA-512:**
```python
hash = hashlib.sha512(password.encode()).hexdigest()
```

**Salted SHA-512:**
```python
salt = secrets.token_hex(16)  # 32-char hex salt
salted_password = password + salt
hash = hashlib.sha512(salted_password.encode()).hexdigest()
```

### Wordlist Pattern Logic

**Generated patterns include:**
- Base elements: names, cities, companies
- Combinations: base + year, base + numbers
- Variations: capitalizations, special characters
- Complex: two-word combinations

**Example combinations:**
```
james              # Base
James              # Capitalized
james1985          # Base + year
James1985          # Capitalized + year
james!             # Base + special char
jamessmith         # Two-word
JamesSmith85       # Complex combination
```

### Performance Benchmarks

| Profiles | Generation Time | Wordlist Entries | Export Size (JSON) |
|----------|----------------|------------------|-------------------|
| 10       | ~1 second      | 200-300          | ~50 KB           |
| 50       | ~3 seconds     | 1,000-1,500      | ~250 KB          |
| 100      | ~5 seconds     | 2,000-3,000      | ~500 KB          |
| 500      | ~20 seconds    | 10,000-15,000    | ~2.5 MB          |
| 1000     | ~40 seconds    | 20,000-30,000    | ~5 MB            |

## Ethical Guidelines

### Educational Use Only

This tool is designed exclusively for:
- Authorized penetration testing
- Cybersecurity education
- Security research
- Password policy development
- Security awareness training

### Prohibited Uses

**DO NOT use this tool for:**
- Unauthorized system access
- Real phishing campaigns
- Impersonating real individuals
- Any illegal activities
- Harassment or stalking

### Legal Considerations

**Always:**
- Obtain written authorization before testing
- Use only on systems you own or have explicit permission to test
- Document all activities
- Follow responsible disclosure practices
- Comply with applicable laws (GDPR, CCPA, etc.)

### Best Practices

1. **Controlled Environment**
   - Use in isolated lab environments
   - Secure all generated data
   - Do not expose data publicly

2. **Documentation**
   - Document educational objectives
   - Record methodology
   - Maintain audit trails

3. **Responsible Use**
   - Explain defensive measures alongside attacks
   - Emphasize legal and ethical boundaries
   - Promote security awareness

### Disclaimer

This tool generates synthetic data for educational purposes only. The authors:
- Are not responsible for misuse
- Do not endorse illegal activities
- Provide this tool "as is" without warranties

**By using this tool, you agree to:**
- Use only for legitimate educational purposes
- Take full responsibility for your actions
- Comply with all applicable laws
- Respect the rights and privacy of others

## Troubleshooting

### Common Issues

**"No profiles to export"**
```bash
# Solution: Generate profiles first
Select option 1 → Generate Profiles
```

**"No salted hashes found"**
```bash
# Solution: Regenerate with salt option
Select option 1 → Choose "Salted SHA-512"
```

**Hashcat shows "All hashes found as potfile"**
```bash
# View cached results
hashcat -m 1710 --show hashes.txt

# Or clear cache and rerun
rm ~/.local/share/hashcat/hashcat.potfile
```

**Can't open exported files (permission denied)**
```bash
# Check permissions
ls -la filename.txt

# Fix permissions
chmod 644 filename.txt
```

**Large datasets take too long**
```bash
# Solution: Use smaller datasets for testing
# 100 profiles recommended for most training scenarios
```

### Performance Tips

**For large datasets (500+):**
- Expect 30-40 seconds for 1000 profiles
- Export to JSON for best performance
- Use CSV for data analysis tools

**For wordlist generation:**
- Larger datasets = larger wordlists (exponential)
- Filter by length or complexity if needed
- Duplicates are automatically removed

## Contributing

Contributions are welcome for educational enhancements:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/enhancement`)
3. Commit changes (`git commit -am 'Add educational feature'`)
4. Push to branch (`git push origin feature/enhancement`)
5. Open a Pull Request

**Please ensure:**
- Educational value of proposed changes
- Ethical use considerations
- Documentation updates
- Code quality standards

## License

**Educational Use License**

Permission is granted to use this tool for educational, research, and authorized security testing purposes only.

**Conditions:**
- Must maintain attribution
- Educational use only
- No commercial use without permission
- No malicious use

**Disclaimer:**
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED. IN NO EVENT SHALL THE AUTHORS BE LIABLE FOR ANY CLAIM, DAMAGES, OR OTHER LIABILITY ARISING FROM THE USE OF THE SOFTWARE.

## Acknowledgments

**Educational Resources:**
- OWASP Password Guidelines
- NIST Digital Identity Guidelines
- CWE-521: Weak Password Requirements

**Tools:**
- Hashcat password cracking framework
- John the Ripper compatibility

**Community:**
- Cybersecurity educators
- Penetration testing professionals
- Security researchers

---

**Author:** zstaigah  
**Version:** 1.0  
**Last Updated:** September 29, 2025  
**Repository:** [GitHub](https://github.com/yourusername/osint-profile-generator)

---

*For educational and authorized security testing purposes only.*
