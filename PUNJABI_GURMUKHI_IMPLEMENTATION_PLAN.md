# Punjabi Gurmukhi Implementation Plan (QWERTY-Based)

## Phase 1: Locale Definition & Registration

### 1.1 Java Code Changes
**File**: `app/src/main/java/rkr/simplekeyboard/inputmethod/latin/utils/SubtypeLocaleUtils.java`

- Add locale constant: `private static final String LOCALE_PUNJABI = "pa";`
- Add to `sSupportedLocales` array in alphabetical order
- Consider regional variant: `LOCALE_PUNJABI_INDIA = "pa_IN"` (following Hindi pattern)

### 1.2 Locale Display Names
**File**: `app/src/main/res/values/strings.xml`
- Add: `<string name="locale_name_pa_IN">Punjabi (India)</string>`

**Files**: All `values-{locale}/strings.xml` files
- Translate "Punjabi (India)" to respective languages following existing pattern

## Phase 2: Keyboard Layout Architecture

### 2.1 Layout Set Definitions
**Files to Create**:
- `app/src/main/res/xml/keyboard_layout_set_gurmukhi.xml` (Traditional)
- `app/src/main/res/xml/keyboard_layout_set_gurmukhi_compact.xml` (Simplified)

**Structure** (following Hindi pattern):
```xml
<KeyboardLayoutSet>
    <Element latin:elementName="alphabet" latin:elementKeyboard="@xml/kbd_gurmukhi" />
    <Element latin:elementName="alphabetAutomaticShifted" latin:elementKeyboard="@xml/kbd_gurmukhi" />
    <Element latin:elementName="alphabetManualShifted" latin:elementKeyboard="@xml/kbd_gurmukhi" />
    <Element latin:elementName="alphabetShiftLocked" latin:elementKeyboard="@xml/kbd_gurmukhi" />
    <!-- Standard symbol layouts -->
</KeyboardLayoutSet>
```

### 2.2 Keyboard Definitions
**Files to Create**:
- `app/src/main/res/xml/kbd_gurmukhi.xml`
- `app/src/main/res/xml/kbd_gurmukhi_compact.xml`

**Features**:
- Number row support (5-row vs 4-row layouts)
- Include common key styles
- Reference Gurmukhi-specific row layouts

## Phase 3: QWERTY-Based Gurmukhi Script Implementation

### 3.1 Row Structure Files
**Files to Create**:
- `app/src/main/res/xml/rows_gurmukhi.xml`
- `app/src/main/res/xml/rows_gurmukhi_compact.xml`

**Layout Design**:
- 3 main character rows + 1 function row (following QWERTY structure)
- Key width: `10%p` (10 keys per row, following QWERTY pattern)
- Font flag: `fontNormal` for proper Gurmukhi rendering

### 3.2 Key Row Definitions
**Files to Create**:
- `app/src/main/res/xml/rowkeys_gurmukhi1.xml` (QWERTY top row)
- `app/src/main/res/xml/rowkeys_gurmukhi2.xml` (ASDF middle row)
- `app/src/main/res/xml/rowkeys_gurmukhi3.xml` (ZXCV bottom row)
- `app/src/main/res/xml/rowkeys_gurmukhi_compact1.xml`
- `app/src/main/res/xml/rowkeys_gurmukhi_compact2.xml`
- `app/src/main/res/xml/rowkeys_gurmukhi_compact3.xml`

### 3.3 QWERTY-to-Gurmukhi Character Mapping

#### **Row 1 (QWERTYUIOP → Gurmukhi)**:
- **Q** → `ਔ` (U+0A14 - GURMUKHI LETTER AU)
- **W** → `ਐ` (U+0A10 - GURMUKHI LETTER AI)  
- **E** → `ਆ` (U+0A06 - GURMUKHI LETTER AA)
- **R** → `ਈ` (U+0A08 - GURMUKHI LETTER II)
- **T** → `ਊ` (U+0A0A - GURMUKHI LETTER UU)
- **Y** → `ਬ` (U+0A2C - GURMUKHI LETTER BA)
- **U** → `ਹ` (U+0A39 - GURMUKHI LETTER HA)
- **I** → `ਗ` (U+0A17 - GURMUKHI LETTER GA)
- **O** → `ਦ` (U+0A26 - GURMUKHI LETTER DA)
- **P** → `ਜ` (U+0A1C - GURMUKHI LETTER JA)

#### **Row 2 (ASDFGHJKL → Gurmukhi)**:
- **A** → `ੋ` (U+0A4B - GURMUKHI VOWEL SIGN OO)
- **S** → `ੇ` (U+0A47 - GURMUKHI VOWEL SIGN EE)
- **D** → `੍` (U+0A4D - GURMUKHI SIGN VIRAMA)
- **F** → `ਿ` (U+0A3F - GURMUKHI VOWEL SIGN I)
- **G** → `ੁ` (U+0A41 - GURMUKHI VOWEL SIGN U)
- **H** → `ਪ` (U+0A2A - GURMUKHI LETTER PA)
- **J** → `ਰ` (U+0A30 - GURMUKHI LETTER RA)
- **K** → `ਕ` (U+0A15 - GURMUKHI LETTER KA)
- **L** → `ਤ` (U+0A24 - GURMUKHI LETTER TA)

#### **Row 3 (ZXCVBNM → Gurmukhi)**:
- **Z** → `ਅ` (U+0A05 - GURMUKHI LETTER A)
- **X** → `ਂ` (U+0A02 - GURMUKHI SIGN BINDI)
- **C** → `ਮ` (U+0A2E - GURMUKHI LETTER MA)
- **V** → `ਨ` (U+0A28 - GURMUKHI LETTER NA)
- **B** → `ਵ` (U+0A35 - GURMUKHI LETTER VA)
- **N** → `ਲ` (U+0A32 - GURMUKHI LETTER LA)
- **M** → `ਸ` (U+0A38 - GURMUKHI LETTER SA)

### 3.4 Gurmukhi-Specific Features

#### **Number System Integration**:
- **Gurmukhi numerals**: ੦ ੧ ੨ ੩ ੪ ੫ ੬ ੭ ੮ ੯ (U+0A66-U+0A6F)
- **QWERTY number row mapping**: 1→੧, 2→੨, 3→੩, etc.
- **Dual number support**: Gurmukhi + Western numerals via long-press
- **Hint labels**: Western numerals (1-0) as hints on character keys

#### **Long-Press More Keys (Traditional Layout)**:
- **Q (ਔ)**: `ਔ,ਔਂ` (AU with Bindi variations)
- **W (ਐ)**: `ਐ,ਐਂ` (AI with Bindi variations)
- **E (ਆ)**: `ਆ,ਆਂ,ਆਁ` (AA with Bindi/Tippi)
- **R (ਈ)**: `ਈ,ਈਂ` (II with Bindi)
- **T (ਊ)**: `ਊ,ਊਂ,ਊਁ` (UU with Bindi/Tippi)
- **I (ਗ)**: `ਗ,ਘ,ਗ਼` (GA, GHA, GHA with nukta)
- **K (ਕ)**: `ਕ,ਖ,ਖ਼` (KA, KHA, KHHA with nukta)
- **J (ਰ)**: `ਰ,ੜ` (RA, RRA)
- **M (ਸ)**: `ਸ,ਸ਼` (SA, SHA with nukta)

#### **Shift State Characters**:
- **Shifted Q**: `ਓ` (GURMUKHI LETTER O)
- **Shifted W**: `ਏ` (GURMUKHI LETTER E)
- **Shifted E**: `ਅ` (GURMUKHI LETTER A)
- **Shifted R**: `ਇ` (GURMUKHI LETTER I)
- **Shifted T**: `ਉ` (GURMUKHI LETTER U)
- **Shifted Y**: `ਭ` (GURMUKHI LETTER BHA)
- **Shifted I**: `ਘ` (GURMUKHI LETTER GHA)
- **Shifted O**: `ਧ` (GURMUKHI LETTER DHA)
- **Shifted P**: `ਝ` (GURMUKHI LETTER JHA)

#### **Special Gurmukhi Characters Access**:
- **Nukta (਼)**: Long-press on period key or dedicated key
- **Tippi (ਂ)**: X key position
- **Adak Bindi (ੰ)**: Long-press on X (Bindi)
- **Virama (੍)**: D key position for conjuncts

## Phase 4: Keystyle System Implementation

### 4.1 Gurmukhi Keystyle Files
**Files to Create** (following Devanagari pattern):
- `app/src/main/res/xml/keystyle_gurmukhi_vowel_sign_aa.xml`
- `app/src/main/res/xml/keystyle_gurmukhi_vowel_sign_i.xml`
- `app/src/main/res/xml/keystyle_gurmukhi_vowel_sign_u.xml`
- `app/src/main/res/xml/keystyle_gurmukhi_vowel_sign_e.xml`
- `app/src/main/res/xml/keystyle_gurmukhi_vowel_sign_o.xml`
- `app/src/main/res/xml/keystyle_gurmukhi_sign_virama.xml`
- `app/src/main/res/xml/keystyle_gurmukhi_sign_bindi.xml`
- `app/src/main/res/xml/keystyle_gurmukhi_sign_nukta.xml`

### 4.2 Layout-Specific Variations
**Structure** (following Hindi pattern):
```xml
<switch>
    <case latin:keyboardLayoutSet="gurmukhi">
        <!-- Traditional layout with full character combinations -->
    </case>
    <case latin:keyboardLayoutSet="gurmukhi_compact">
        <!-- Simplified layout with grouped characters -->
    </case>
</switch>
```

### 4.3 API Compatibility
- Include dotted circle (U+25CC) hack for API < 16
- Separate `-v16` versions for modern Android versions

## Phase 5: Localization & Cultural Adaptation

### 5.1 Punjabi UI Translation
**File to Create**: `app/src/main/res/values-pa/strings.xml`

**Key Translations**:
- `vibrate_on_keypress` → "ਕੀ ਦਬਾਉਣ 'ਤੇ ਵਾਈਬਰੇਟ"
- `sound_on_keypress` → "ਕੀ ਦਬਾਉਣ 'ਤੇ ਆਵਾਜ਼"
- `settings_screen_preferences` → "ਤਰਜੀਹਾਂ"
- `auto_cap` → "ਆਪਣੇ ਆਪ ਵੱਡੇ ਅੱਖਰ"
- `select_language` → "ਭਾਸ਼ਾਵਾਂ"
- `subtype_traditional` → "ਰਵਾਇਤੀ"
- `subtype_compact` → "ਸੰਖੇਪ"

### 5.2 Regional Variants
**Consider adding**:
- `pa_IN` (Punjabi India) - Primary implementation
- `pa_PK` (Punjabi Pakistan) - If Shahmukhi script support needed later

### 5.3 Punctuation & Spacing
**File to Create**: `app/src/main/res/values-pa/donottranslate-config-spacing-and-punctuations.xml`

**Gurmukhi-specific settings**:
- Sentence separator configuration
- Word boundary definitions
- Punctuation spacing rules

## Phase 6: Layout Variants & User Experience

### 6.1 Traditional vs Compact Layouts

#### **Traditional Layout Features**:
- Complete QWERTY-mapped Gurmukhi character set
- Full vowel sign combinations with Bindi/Tippi via long-press
- All nukta variants accessible via long-press
- Shift state support for vowel letters
- Conjunct consonant support via Virama

#### **Compact Layout Features**:
- Grouped aspirated consonants (ਕ/ਖ, ਗ/ਘ, ਚ/ਛ, etc.) on single keys
- Essential vowel signs with simplified access
- Common nukta variants as primary more keys
- Beginner-friendly QWERTY familiarity
- Reduced long-press complexity

### 6.2 Number Row Integration
- **5-row mode**: Dedicated number row with Gurmukhi numerals (੧੨੩...)
- **4-row mode**: Number hints (1,2,3...) on QWERTY character keys
- **Dual number system**: Both Gurmukhi and Western numerals accessible

### 6.3 QWERTY Familiarity Benefits
- **Muscle memory**: Users familiar with English QWERTY can adapt quickly
- **Consistent positioning**: Character positions remain predictable
- **Standard layout**: Follows established QWERTY key arrangement (10-10-7 keys)

## Implementation Priority Order

1. **Core Infrastructure** (Phase 1-2): Locale registration and basic QWERTY-based layout structure
2. **QWERTY Character Mapping** (Phase 3): Implement traditional layout with QWERTY positioning
3. **Keystyle System** (Phase 4): Create reusable character combination logic
4. **Compact Layout** (Phase 3.2): Simplified QWERTY version for broader accessibility
5. **Localization** (Phase 5): Punjabi UI and cultural adaptations

This QWERTY-based plan ensures **familiar layout positioning** while providing comprehensive Punjabi Gurmukhi support that aligns with Simple Keyboard's architecture and user expectations from English keyboard layouts.