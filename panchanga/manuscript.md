# Panchanga as a Classical Indian Calendar and Astronomical Knowledge System

## The five limbs of time, local astronomy, regional convention, and responsible digital calculation

### Abstract

Panchanga is often translated as “Hindu calendar,” but the term more precisely denotes a five-limbed almanac that coordinates civil dates with astronomical and calendrical quantities. Its five principal elements are vara (weekday), tithi (lunar day), nakshatra (lunar mansion), yoga (a luni-solar angular sum), and karana (half of a tithi). A working panchanga normally includes much more: sunrise and sunset, moonrise and moonset, solar and lunar months, planetary positions, eclipses, festivals, and rules for applying astronomical intervals to local observance.

This paper studies Panchanga as a classical Indian astronomical and calendrical knowledge system. It explains the mathematical structure of the five limbs, the role of true solar and lunar longitude, the difference between tropical and sidereal frames, and the reason location and sunrise can change a displayed result. It also distinguishes computed astronomical data from inherited naming systems, regional calendar conventions, ritual selection rules, and astrological interpretation. The modern history of the Calendar Reform Committee, the Indian Astronomical Ephemeris, and the Rashtriya Panchang shows that accurate computation does not erase cultural plurality: a standard ephemeris can coexist with Amanta and Purnimanta lunar months, regional solar calendars, and observance rules keyed to sunrise, moonrise, midnight, or another defined time.

The paper concludes with a framework for responsible digital publication. A trustworthy Panchanga service should disclose location, time zone, ayanamsa, ephemeris, day-boundary convention, event-selection rule, and uncertainty near transitions. It should cache and reuse calculations without pretending that one pan-Indian clock time is valid everywhere. Panchanga is therefore best understood neither as a list of auspicious labels nor as astronomy alone, but as a layered interface between celestial calculation, calendrical convention, textual tradition, and lived practice.

---

## Executive summary

- **Panchanga means “five-limbed.”** The five limbs are vara, tithi, nakshatra, yoga, and karana. Modern almanacs commonly add sunrise, sunset, lunar and solar months, planetary positions, festivals, and other data [1](https://packolkata.imd.gov.in/panchang/en/explanation).
- **Four limbs depend directly on angular relations involving the Sun and Moon.** Tithi divides elongation between Moon and Sun into 30 parts of 12 degrees. Karana divides a tithi into two 6-degree halves. Nakshatra divides sidereal lunar longitude into 27 parts of 13 degrees 20 minutes. Yoga divides the normalized sum of sidereal solar and lunar longitude into 27 equal parts.
- **A weekday is simple only after the day boundary is declared.** Civil systems change date at midnight. Many panchanga presentations associate the religious day with local sunrise. A software service must say which convention it uses.
- **A tithi is not a fixed 24-hour day.** Because the relative motion of Sun and Moon varies, a tithi can begin or end at any clock time. The Rashtriya Panchang gives a mean duration of about 23 hours 37 minutes and a broad actual range [2](https://packolkata.imd.gov.in/panchang/en/astronomical-info).
- **Location matters.** The astronomical instant of a longitude boundary is global, but its local clock representation, sunrise relation, moonrise relation, and civil date depend on time zone and coordinates. Near a transition, two cities can assign a different sunrise tithi or nakshatra.
- **Astronomy and observance rules are separate layers.** An ephemeris can calculate a tithi boundary precisely. A festival rule decides which civil day receives the observance when the tithi touches one or more relevant times.
- **Regional difference is not automatically error.** Amanta and Purnimanta lunar months label part of the same lunar sequence differently. Tamil, Malayalam, Bengali, and other solar calendars apply their own month-boundary conventions while also using tithi and nakshatra.
- **Modern standardization has a specific history.** The Calendar Reform Committee chaired by Meghnad Saha recommended a national calendar and modern ephemerides. The Positional Astronomy Centre now publishes the Indian Astronomical Ephemeris and Rashtriya Panchang using modern astronomical formulae [3](https://mausam.imd.gov.in/responsive/indianAstronomicalEphemeris.php) [4](https://packolkata.imd.gov.in/panchang/en/preface).
- **Digital Panchanga requires reproducibility.** A result should record date, time, latitude, longitude, time zone, ephemeris, ayanamsa, computational precision, and the rule used to turn intervals into a named day.
- **Interpretation should be labelled.** Computed positions and intervals are reproducible astronomical data. Claims about auspiciousness, personality, or predicted events belong to interpretive traditions and should not be presented as astronomical measurements.

---

## 1. Scope, method, and limits

This paper addresses four connected questions:

1. What are the five limbs of Panchanga?
2. How are those limbs derived from astronomical quantities?
3. Why can calendars disagree even when their calculations are competent?
4. What should a responsible digital Panchanga disclose?

The method is source-led and layered. Current computational practice is documented primarily through the Positional Astronomy Centre of the India Meteorological Department, which publishes the Indian Astronomical Ephemeris and Rashtriya Panchang. Historical standardization is read through the 1955 *Report of the Calendar Reform Committee*. Classical astronomical context is approached through the received *Surya Siddhanta* and scholarship on Indian calendrical astronomy. Existing regional practice is described as convention rather than reduced to one uniform national rule.

Several limits are important. This is not a manual for selecting a muhurta, fixing temple observances, or overriding a family or sampradaya calendar. It does not claim that all Indian calendars use one textual authority, ayanamsa, sunrise definition, or festival rule. It also does not treat the present wording of a classical text as an unchanged document from a single date. Mathematical astronomy, textual transmission, ritual jurisprudence, and regional usage each have their own evidence.

The paper uses “astronomical” for quantities derived from celestial positions and time. It uses “calendrical” for conventions that organize those quantities into days, months, and years. It uses “ritual rule” for the criterion that assigns an observance to a civil date. These layers interact, but they should not be collapsed.

## 2. What Panchanga means

The Sanskrit compound *pañcāṅga* combines *pañca*, five, and *aṅga*, limb or component. The five limbs conventionally listed in almanac literature are:

| Limb | Working meaning | Primary quantity |
| --- | --- | --- |
| Vara | Weekday | Local day in a seven-day cycle |
| Tithi | Lunar day | Each 12-degree interval of Moon-Sun elongation |
| Nakshatra | Lunar mansion | Each 13 degrees 20 minutes of sidereal lunar longitude |
| Yoga | Luni-solar combination | Each 13 degrees 20 minutes of the normalized sum of sidereal Sun and Moon longitude |
| Karana | Half-tithi | Each 6-degree interval of Moon-Sun elongation |

The phrase “five limbs” does not mean that an almanac contains only five fields. The Rashtriya Panchang also presents sunrise, sunset, moonrise, moonset, Julian day, Kali ahargana, Moon age, declination, sidereal time, equation of time, rashi and nakshatra transits, and festival information [1](https://packolkata.imd.gov.in/panchang/en/explanation). Printed regional panchangas may include muhurta tables, eclipses, sankranti, fasts, temple observances, planetary positions, and interpretive material.

Panchanga is therefore both a compact mathematical coordinate system for a moment and a publication genre. The five limbs identify the calendrical state; the almanac places that state within a larger social, ritual, and regional schedule.

## 3. Astronomical foundations: longitude, motion, and reference frames

Most Panchanga calculations begin with the apparent geocentric positions of the Sun and Moon along the ecliptic. Longitude expresses a position around the 360-degree ecliptic circle. The key operations are subtraction, addition, normalization to a 0-360 degree range, and division into equal segments.

Two reference frames must be distinguished:

- **Tropical longitude** uses the moving vernal equinox as zero.
- **Sidereal or nirayana longitude** uses a fixed stellar reference, obtained in common modern practice by subtracting an ayanamsa from tropical longitude.

The ayanamsa represents the angular separation between tropical and sidereal origins. Different ayanamsa definitions can produce slightly different sidereal longitudes. Most results remain in the same segment, but a Moon close to a nakshatra boundary can change classification when a different setting is used. A reliable service therefore records the chosen ayanamsa rather than presenting “sidereal” as a complete specification.

The Rashtriya Panchang describes a variable ayanamsa and a fixed initial point tied to its adopted reference [1](https://packolkata.imd.gov.in/panchang/en/explanation). Contemporary software may use Lahiri/Chitrapaksha or another named definition. The correct engineering question is not “Which setting is universally Indian?” but “Which setting does this result claim to use, and can the result be reproduced?”

The astronomical positions also depend on an ephemeris: a model or data set that gives celestial positions for time. The Indian Astronomical Ephemeris is designed to provide astronomical data for observers and Panchanga makers and uses modern astronomical standards [3](https://mausam.imd.gov.in/responsive/indianAstronomicalEphemeris.php). Other software may use JPL-derived ephemerides or established astronomical libraries. Differences of seconds or minutes near a boundary can arise from model, interpolation, delta-T, topocentric correction, refraction, precision, and rounding choices.

## 4. The five limbs in calculation

### 4.1 Vara: weekday and the definition of a day

Vara is the weekday in the seven-day sequence. For an ordinary civil timestamp, weekday is derived from the local calendar date. In ritual or almanac usage, however, the day may be associated with local sunrise rather than midnight. A pre-dawn time can therefore belong to one civil date but still be discussed under the preceding sunrise day in a traditional schedule.

This is not an astronomical contradiction. It is a boundary convention. Digital interfaces should display the civil date and explain whether “today’s vara” means the weekday at the selected timestamp or the sunrise-based religious day.

### 4.2 Tithi: the lunar day

Let the normalized apparent longitudes of Moon and Sun be `L_m` and `L_s`. Define elongation:

**Elongation:** `E = (Moon longitude - Sun longitude) modulo 360 degrees`

The tithi number is:

**Tithi number:** `floor(E / 12 degrees) + 1`

Thirty tithis complete a synodic month. Tithis 1-15 form the waxing or Shukla Paksha; tithis 16-30 form the waning or Krishna Paksha when numbered continuously, though traditional naming restarts from Pratipada in each paksha. Purnima corresponds to the full-moon boundary and Amavasya to the completion of the waning cycle.

A tithi is an angular interval, not a fixed 24-hour period. Sun and Moon do not move at perfectly uniform apparent rates, so the duration varies. The Rashtriya Panchang lists a mean tithi duration of approximately 23 hours 37 minutes and notes a much wider actual range [2](https://packolkata.imd.gov.in/panchang/en/astronomical-info). A tithi can begin at 2:17 p.m., end before the next sunrise, span two sunrises, or be absent at sunrise on a civil date.

This produces two familiar calendar phenomena:

- **Vriddhi or repeated tithi:** the same tithi is present at two successive sunrises.
- **Kshaya or omitted sunrise tithi:** a short tithi begins and ends between two sunrises, so it is not the sunrise tithi of either day.

The tithi still existed. It was simply not current at sunrise.

### 4.3 Karana: half of a tithi

A karana spans 6 degrees of Moon-Sun elongation. There are 60 karana intervals in a synodic month but only 11 traditional names because seven movable karanas repeat and four fixed karanas occur at designated positions near the end and beginning of the cycle.

Computationally, karana is a finer division of the same elongation used for tithi:

**Karana interval:** `floor(E / 6 degrees)`

Mapping the interval index to a traditional name requires the inherited sequence rule. This illustrates a recurring distinction: geometry determines the interval; calendrical tradition supplies the name sequence.

### 4.4 Nakshatra: the lunar mansion

In the common 27-fold system, the sidereal ecliptic is divided into equal segments of 13 degrees 20 minutes. If `L_m,sid` is sidereal lunar longitude:

**Nakshatra number:** `floor(sidereal Moon longitude / 13 degrees 20 minutes) + 1`

Ashwini begins the sequence, followed by Bharani, Krittika, and the remaining mansions through Revati. Each nakshatra has four padas of 3 degrees 20 minutes. A nakshatra in modern Panchanga calculation is therefore a longitude segment, not one physical star. Named stars or asterisms provide historical and observational associations, while the computational grid covers the whole ecliptic.

Because the Moon’s motion varies, nakshatra duration varies. The Rashtriya Panchang gives a mean duration of about 24 hours 17 minutes [2](https://packolkata.imd.gov.in/panchang/en/astronomical-info). A transition can occur at any local time.

### 4.5 Yoga: the luni-solar sum

The 27 nitya yogas are derived from the normalized sum of sidereal solar and lunar longitude:

**Yoga sum:** `(sidereal Moon longitude + sidereal Sun longitude) modulo 360 degrees`

**Yoga number:** `floor(yoga sum / 13 degrees 20 minutes) + 1`

This yoga should not be confused with Yoga as a philosophical discipline or with every other use of the word “union.” Here it is a specific calendrical angular quantity with an inherited sequence of 27 names.

## 5. From an instant to a daily Panchanga

An ephemeris can answer “What tithi is running at this instant?” A daily Panchanga must answer additional questions:

- Which tithi is current at local sunrise?
- At what local clock time does it end?
- Does the next tithi also end before the following sunrise?
- Which nakshatra, yoga, and karana are current at sunrise?
- Which transitions occur during the civil date?
- Which month, paksha, and year labels apply under the selected system?

A robust algorithm calculates intervals around the required date rather than sampling only at noon or midnight. It locates each angular boundary using numerical root finding or sufficiently precise interpolation, converts the event instant to the requested time zone, and then applies the publication’s day rule.

Sunrise must also be calculated for the coordinates and date. Sunrise is not the same clock time throughout India and is affected by latitude, longitude, date, elevation, atmospheric refraction assumptions, and the adopted definition of the solar limb. The Rashtriya Panchang explicitly describes sunrise and sunset as apparent upper-limb events and supplies station-specific data and correction material [1](https://packolkata.imd.gov.in/panchang/en/explanation).

The resulting daily record should retain both machine-readable instants and human-readable labels. Storing only “Rohini until 4:20 PM” without date, offset, coordinates, and computational settings prevents later audit.

## 6. Why location changes the answer

The geocentric instant at which lunar elongation reaches a tithi boundary is nearly the same worldwide. What changes is its relationship to local civil time and local sunrise.

Consider a boundary at 00:45 UTC. It appears as the previous evening in New York, early morning in London, morning in India, and late morning in Singapore. If the boundary falls near sunrise, one city may begin the day with the earlier tithi while another begins with the next. The same principle applies to nakshatra, yoga, and karana.

Location affects:

1. the time-zone conversion of a global event;
2. the local civil date containing the event;
3. sunrise and sunset;
4. moonrise and moonset;
5. topocentric quantities when they are used;
6. which interval is present at the rule’s required local time.

This is why “today’s tithi in India” is a useful approximation but not a complete ceremonial answer. Many Indian cities will agree on most days, yet a transition near sunrise can produce a real difference. International visitors require local calculations rather than a simple conversion of a Delhi calendar.

## 7. Lunar months, solar months, and regional calendars

Panchanga operates within several calendar layers.

### 7.1 Amanta and Purnimanta

In an Amanta system, the lunar month ends with Amavasya. In a Purnimanta system, it ends with Purnima. The tithi sequence and Moon phase do not change, but part of the waning fortnight receives a different month label. A Krishna Ashtami can therefore carry neighbouring month names in two regional traditions without either changing the underlying elongation.

### 7.2 Solar months

Tamil, Malayalam, Bengali, and other regional calendars commonly use solar month systems tied to the Sun’s passage through sidereal signs, with local rules for assigning the transition to a civil date. These month names are not merely translations of lunar months. A regional Panchanga can display a solar month, a lunar tithi, a nakshatra, and a Gregorian date together because they are different coordinate layers.

### 7.3 Intercalation

A lunisolar calendar must reconcile about 12 synodic months with the solar year. Adhika masa is introduced under a rule connected with the absence of a solar ingress during a lunar month. Rare contrary cases and regional naming conventions require careful treatment. The important methodological point is that intercalation is rule-based, not an arbitrary adjustment added by a website.

## 8. Festival dates: astronomical data plus selection rules

Festival selection is not produced by tithi name alone. A rule may ask which civil day contains a tithi at sunrise, moonrise, midday, sunset, midnight, or a defined pre-dawn interval. It may prefer the first or second day when a tithi spans two relevant times. It may also involve nakshatra, solar month, weekday, or regional textual authority.

The workflow is:

1. calculate the relevant astronomical intervals;
2. calculate local sunrise, moonrise, or another required event;
3. apply the named observance rule;
4. label the result for the regional or sectarian tradition;
5. disclose when another recognized rule produces a different civil date.

This distinction explains why two calendars can agree on the exact tithi ending time yet place a vrata on different dates. Vaishnava Ekadashi rules involving arunodaya and tithi purity are not identical to a simple sunrise-tithi rule. Janmashtami can involve Ashtami and Rohini around midnight under tradition-specific criteria. Karva Chauth involves moonrise. Shivaratri emphasizes a night interval. A generic “all festivals use sunrise” rule is therefore inaccurate.

For users, the safest interface presents the calculated intervals and names the selection convention. For important rites, it should advise confirmation with the relevant temple, family, or sampradaya calendar.

## 9. Classical astronomy and the living computational tradition

Indian calendrical astronomy developed through a long textual and practical tradition. The *Vedanga Jyotisha* belongs to an early phase of calendrical reckoning organized around lunar mansions and a lunisolar cycle. Siddhanta literature developed mathematical models for celestial motion, time, eclipses, and related calculation. Karana texts and astronomical tables provided practical procedures for working calculators.

The received *Surya Siddhanta* is one influential work in this history, but it should not be treated as the single timeless source of every Panchanga rule. Its text has a transmission history, and regional astronomical lineages also used works associated with Aryabhata, Brahmagupta, Bhaskara, and later authors. Table traditions could update parameters, apply corrections, or follow distinct schools.

The practical Panchanga is therefore a meeting point of theory, tables, observation, inherited constants, local correction, and ritual rules. Historical study asks which parameters and procedures a calculator used. Modern production asks whether the chosen ephemeris and algorithms accurately represent the declared standard.

## 10. Calendar reform and the Rashtriya Panchang

By the mid-twentieth century, divergent parameters and computational practices produced substantial disagreement among Indian almanacs. The Government of India appointed the Calendar Reform Committee in 1952 under Meghnad Saha. Its 1955 report examined existing calendars and recommended a unified national civil calendar, a modern Indian ephemeris, and standardized astronomical data [5](https://dspace.gipe.ac.in/xmlui/bitstream/handle/10973/39692/GIPE-043972.pdf?isAllowed=y&sequence=3).

The resulting institutional programme did not abolish regional religious calendars. It established a modern national infrastructure. The Positional Astronomy Centre prepares astronomical data for scientific and calendrical purposes, including festival information for Panchanga makers [6](https://mausam.imd.gov.in/responsive/servicesPosAstro.php). The Rashtriya Panchang has been published since 1957-58 and is now available in multiple Indian languages [4](https://packolkata.imd.gov.in/panchang/en/preface).

Its significance is methodological:

- modern astronomical formulae can supply accurate positions and transitions;
- a national reference can document its origin, ayanamsa, station, and timing conventions;
- festival and calendar rules still require explicit definition;
- regional calendars remain culturally and practically important.

Standardization should therefore be understood as improved reproducibility, not the elimination of every legitimate convention.

## 11. Calculation is not interpretation

A Panchanga can calculate that the Moon is in a specified nakshatra, that a tithi ends at a particular instant, or that sunrise occurs at a given local time under declared assumptions. These are astronomical or calendrical outputs.

Statements that a yoga is fortunate, a karana forbids an activity, or a nakshatra predicts an outcome belong to astrological, ritual, or cultural interpretation. They can be documented as traditional teachings, but they are not measurements produced by the longitude formula itself.

Responsible publication uses labels such as:

- **Computed:** position, interval, transition, sunrise, moonrise.
- **Calendrical convention:** month name, sunrise-day assignment, intercalation rule.
- **Observance rule:** the criterion choosing a festival or vrata date.
- **Traditional interpretation:** auspiciousness, deity association, recommended or avoided activity.

This vocabulary allows both lay readers and technically trained readers to see what kind of claim they are evaluating.

## 12. A framework for responsible digital Panchanga publication

### 12.1 Minimum reproducibility metadata

Every generated result should retain:

- requested local date and time;
- latitude, longitude, and location label;
- IANA time zone and UTC offset at the event;
- ephemeris or astronomical library version;
- tropical-to-sidereal setting and ayanamsa;
- geocentric or topocentric choice where relevant;
- sunrise definition and atmospheric assumptions;
- numerical precision and rounding policy;
- day-boundary and festival-selection convention;
- generation time and cache version.

### 12.2 Efficient architecture

Calendar pages should not issue dozens of identical external requests during a visitor’s first load. A sound service can:

1. calculate or request multiple dates in one batch;
2. cache immutable historical results for long periods;
3. cache future results with versioned keys tied to the algorithm;
4. reuse one Indian reference calculation for display rows that intentionally share a convention, while calculating genuinely location-dependent sunrise and international results separately;
5. precompute high-demand pages;
6. serve a complete, indexable response without waiting for browser-side lazy loading;
7. fail transparently with previously verified cached data rather than inventing “date pending” results.

Caching does not reduce astronomical validity when the input and algorithm are unchanged. It improves availability and protects upstream services from rate-limit failure.

### 12.3 User-facing uncertainty

Near a transition, a few minutes can matter. Interfaces should show full date, time, and zone; avoid hiding a next-day ending time behind a clock-only label; and state when rounding could move a displayed minute. If a result is unavailable, the page should distinguish a service failure from an astronomical absence.

### 12.4 Search and accessibility

An indexable calendar page should contain a descriptive heading, direct answer, date, location, structured data, explanatory text, and crawlable previous/next links. Tables need captions and header associations. Controls need accessible names and keyboard operation. Images should be optional explanatory assets, not the sole carrier of a date or time.

## 13. Reading a daily Panchanga: a practical sequence

For a clear reading, use this order:

1. **Confirm location and time zone.** A saved city name without coordinates or zone is insufficient.
2. **Check sunrise.** This anchors the common sunrise-day presentation.
3. **Read tithi and its end time.** Note whether the end falls today or after midnight.
4. **Read nakshatra and its transition.** Distinguish today’s transit nakshatra from a person’s birth nakshatra.
5. **Read yoga and karana.** Treat them as calculated limbs before applying any traditional interpretation.
6. **Check the lunar and solar month labels.** Identify whether the lunar system is Amanta or Purnimanta and which regional solar calendar is displayed.
7. **For a festival, inspect its rule.** Sunrise, moonrise, midnight, or another interval may govern.
8. **For a ceremony, confirm the tradition.** A public digital tool is educational and cannot replace a temple or family authority for every observance.

This sequence prevents a common error: copying one time from a social image without knowing its city, year, time zone, or rule.

## 14. Conclusion

Panchanga is a compact but sophisticated interface between astronomy and culture. Its five limbs are mathematically defined, yet a useful almanac cannot be produced by five divisions alone. It needs an ephemeris, a reference frame, a location, a time standard, sunrise and other local events, month conventions, festival rules, textual interpretation, and editorial judgment.

The tradition’s plurality should not be used as an excuse for vague calculation. Nor should computational precision be used to erase regional practice. The strongest modern approach is explicit layering: accurate celestial positions, reproducible segment boundaries, named calendar conventions, documented observance rules, and clearly labelled interpretation.

When these layers are visible, Panchanga becomes more intelligible to both everyday users and specialists. A reader can see why two cities sometimes differ, why a tithi is not a 24-hour date, why the same lunar fortnight can carry different month labels, and why a festival decision requires more than a generic API response. This transparency is the foundation for responsible digital preservation and publication of Indian calendrical knowledge.

---

## Research and editorial disclosure

This paper is an educational study of calendrical astronomy, textual tradition, and digital publication. It is not a personal horoscope, muhurta prescription, or substitute for a temple, family, or sampradaya calendar. Formulae are explanatory and implementations should be validated against a declared ephemeris and trusted reference data. Historical statements, current institutional standards, computed astronomical quantities, and traditional interpretations are identified as distinct evidence layers.

The publication has not undergone external academic peer review. Corrections, source clarifications, and documented computational disagreements are welcome through Vedic Matters. Material revisions will be recorded through versioned releases.

## References

1. Positional Astronomy Centre, India Meteorological Department. “Details of the Panchang.” *Rashtriya Panchang, Saka Era 1948 (2026-27).* https://packolkata.imd.gov.in/panchang/en/explanation
2. Positional Astronomy Centre, India Meteorological Department. “Various Astronomical Information.” *Rashtriya Panchang.* https://packolkata.imd.gov.in/panchang/en/astronomical-info
3. India Meteorological Department. “The Indian Astronomical Ephemeris.” https://mausam.imd.gov.in/responsive/indianAstronomicalEphemeris.php
4. Positional Astronomy Centre, India Meteorological Department. “Preface.” *Rashtriya Panchang.* https://packolkata.imd.gov.in/panchang/en/preface
5. Calendar Reform Committee, Government of India. *Report of the Calendar Reform Committee.* New Delhi: Council of Scientific and Industrial Research, 1955. https://dspace.gipe.ac.in/xmlui/bitstream/handle/10973/39692/GIPE-043972.pdf?isAllowed=y&sequence=3
6. India Meteorological Department. “Positional Astronomy.” https://mausam.imd.gov.in/responsive/servicesPosAstro.php
7. Positional Astronomy Centre, India Meteorological Department. *Rashtriya Panchang, Saka Era 1948, 2026-27.* https://packolkata.imd.gov.in/panchang/
8. Ikeyama, Setsuro, and Kim Plofker. “The Tithicintamani of Ganesa, a Medieval Indian Treatise on Astronomical Tables.” *SCIAMVS* 2 (2001): 251-289. https://www.sciamvs.org/files/SCIAMVS_02_251-289_Ikeyama_Plofker.pdf
9. Burgess, Ebenezer, trans. *Translation of the Surya Siddhanta.* Journal of the American Oriental Society 6 (1860). https://upload.wikimedia.org/wikipedia/commons/7/7d/Translation_of_the_Surya_Siddhanta_%28IA_pli.kerala.rare.11437%29.pdf
10. Ohashi, Yukio. “Development of Astronomical Observations in Vedic and Post-Vedic India.” *Indian Journal of History of Science* 28, no. 3 (1993). Indian National Science Academy archive.
11. Saha, Meghnad, and N. C. Lahiri. “History of the Calendar in Different Countries through the Ages.” In *Report of the Calendar Reform Committee.* CSIR, 1955.
12. Vedic Matters Editorial Team. “How to Read Your Daily Panchanga Report.” https://vedicmatters.com/article/how-to-read-your-daily-panchanga-report/jyothi-sasthra
13. Vedic Matters. “Today’s Tithi.” https://vedicmatters.com/tithi
14. Vedic Matters. “Today’s Nakshatra.” https://vedicmatters.com/nakshatra
15. Vedic Matters. “Daily Panchanga.” https://vedicmatters.com/panchanga
