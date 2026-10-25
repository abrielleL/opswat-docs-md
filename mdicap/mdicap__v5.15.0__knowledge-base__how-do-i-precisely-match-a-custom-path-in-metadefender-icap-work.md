<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/how-do-i-precisely-match-a-custom-path-in-metadefender-icap-work -->

# How do I precisely match a custom path in MetaDefender ICAP workflow filters by escaping the % character?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Check Your Version:**

This article applies to all MetaDefender ICAP V5 releases deployed on Windows systems.

## [**Summary**](/docs/mdicap/v5.15.0/knowledge-base/how-do-i-precisely-match-a-custom-path-in-metadefender-icap-work#summary)

When you type a filter that includes a literal `%2F` sequence, MetaDefender ICAP’s glob-matching filter logic may treat `%xx` as an encoding pattern (so the `%` is not handled as a literal character). The reliable way to match a literal percent sign is to use a **glob character class** that contains only `%`: `[%]`. MetaDefender ICAP’s wildcard matching (glob) explicitly supports character classes like `[ab]`.

## [**Symptoms**](/docs/mdicap/v5.15.0/knowledge-base/how-do-i-precisely-match-a-custom-path-in-metadefender-icap-work#symptoms)

- The request “HTTP URL” appears as: `/%2FSESDATA%2Ffile.txt`
- Filters like `/%2FSESDATA%2F*` do **not** match
- A workaround like `/?2FSESDATA?2F*` **does** match (because `?` matches the single `%` character)

## [**Examples:**](/docs/mdicap/v5.15.0/knowledge-base/how-do-i-precisely-match-a-custom-path-in-metadefender-icap-work#examples)

`/%252FSESDATA%252F*` -> Does not work

`/%2FSESDATA%2F*` -> Does not work

`//SESDATA/` -> Does not work

`/?2FSESDATA?2F*` -> Works, but is not able to target that percentage character without using a single character wildcard.

## [**Resolution (precise match without** `?`**)**](/docs/mdicap/v5.15.0/knowledge-base/how-do-i-precisely-match-a-custom-path-in-metadefender-icap-work#resolution-precise-match-without-)

1. Go to **Policy → Security rules** and **Edit** (or create) the relevant security rule.
2. In **Request filter**, add/edit the condition that uses **Wildcard matching (glob)** (for example, **Host IP/Domain conditions** if that is where the URL/URI is available in your deployment).
3. Set the pattern to **escape the percent sign** using a character class:

   - **For all objects under SESDATA**:

     - `/%[%]2FSESDATA[%]2F*`
     - (commonly written without the extra `%` character as): `/%2F...` → use `[%]2F...` for the `%` portion
   - **Example (what worked in practice)**:

     - `/[%]2FSESDATA[%]2F*`
4. Save the rule, and ensure it is placed **above** any broader/default rule (MetaDefender ICAP uses a **first match policy**).
5. Re-test with a request such as `/%2FSESDATA%2Ffile.txt` and confirm the request is routed to the intended workflow.

**Why this works:** MetaDefender ICAP glob matching supports bracket expressions such as `[ab]` (matches one character from the set). Therefore `[%]` matches **exactly one character**, and that character must be `%`.

## [**Alternative (if you need a fully deterministic selector)**](/docs/mdicap/v5.15.0/knowledge-base/how-do-i-precisely-match-a-custom-path-in-metadefender-icap-work#alternative-if-you-need-a-fully-deterministic-selector)

If URL normalization/encoding makes URL-based matching unreliable in a given environment, route workflows using a **header you control** (added by the proxy / ICAP client), then filter on that header value. MetaDefender ICAP explicitly supports workflow filtering based on request headers, and also supports encapsulated custom headers (e.g., `X-Client-Custom-*`) when enabled.

**Steps (header-based routing):**

1. Configure the proxy/ICAP client to add a request header such as `X-Target-Folder: SESDATA`.
2. In the security rule’s **Request filter**, add a **generic condition** matching that header (e.g., equals `SESDATA`).

If **Further Assistance** is required, please proceed to log a [support case or chat with one of our support engineers](https://my.opswat.com/support).
