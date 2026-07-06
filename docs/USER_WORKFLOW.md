# KAL — მომხმარებლის სამუშაო პროცესი

## როდესაც ცვლილებას AI აკეთებს

AI-მ სამუშაოს დასრულებამდე თვითონ უნდა გაუშვას:

```powershell
npm run ai:sync
npm run ai:validate
```

- `ai:sync` აახლებს პროექტის რუკას, AI adapter-ებს, skill-ებს და MCP კონფიგურაციას.
- `ai:validate` ამოწმებს, რომ KAL სინქრონიზებულია და ყველა contract test გადის.

კოდის ტიპის მიხედვით AI-მ დამატებით უნდა გაუშვას შესაბამისი project validation, მაგალითად:

```powershell
npm run prepack
```

თუ validation ვერ გაივლის, AI-მ უნდა წაიკითხოს ზუსტი შეცდომა, გაასწოროს მხოლოდ root cause და იგივე validation თავიდან გაუშვას.

შენგან საჭიროა მხოლოდ შედეგისა და ცვლილებების გადახედვა:

```powershell
git status
git diff
```

თუ შედეგი სწორია, შეინახე Git-ში:

```powershell
git add .
git commit -m "მოკლე ცვლილების აღწერა"
git push
```

## როდესაც ცვლილებას ადამიანი აკეთებს

ხელით კოდის, კონფიგურაციის, policy-ის, skill-ის ან MCP registry-ის შეცვლის შემდეგ გაუშვი:

```powershell
npm run ai:sync
npm run ai:validate
```

შემდეგ გაუშვი შეცვლილ ფუნქციასთან დაკავშირებული project validation. ამ პროექტში ძირითადი package შემოწმებაა:

```powershell
npm run prepack
```

UI ცვლილებისას გაუშვი development server და შედეგი ბრაუზერში შეამოწმე:

```powershell
npm run dev
```

თუ ყველაფერი სწორია:

```powershell
git status
git diff
git add .
git commit -m "მოკლე ცვლილების აღწერა"
git push
```

## რომელი ბრძანება რისთვისაა

| ბრძანება | დანიშნულება | ვინ უშვებს |
|---|---|---|
| `npm run ai:sync` | generated KAL ფაილების განახლება | AI ავტომატურად; ადამიანი ხელით ცვლილების შემდეგ |
| `npm run ai:validate` | KAL sync/schema/tests შემოწმება | AI ავტომატურად; ადამიანი ხელით ცვლილების შემდეგ |
| `npm run ai:check` | მხოლოდ generated ფაილებისა და კონფიგურაციის შემოწმება | ჩვეულებრივ `ai:validate`-ის ნაწილი |
| `npm run ai:test` | KAL contract tests | ჩვეულებრივ `ai:validate`-ის ნაწილი |
| `npm run ai:assess -- --request "დავალება" --files path1,path2` | დავალების complexity-ის შეფასება | ძირითადად AI ან debugging-ისას ადამიანი |
| `npm run prepack` | Svelte package-ის შემოწმება | AI ცვლილების შემდეგ; საჭიროებისას ადამიანი |
| `npm run dev` | პროექტის ლოკალურად გაშვება | UI/ქცევის ხელით სანახავად |
| `npm run mcp:project` | Project MCP server-ის ხელით გაშვება | მხოლოდ MCP host-ის პირდაპირი კონფიგურაციისას |

## მნიშვნელოვანი წესები

- generated ფაილები ხელით არ შეცვალო: `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, `PROJECT_MAP.md`, `.mcp.json` და vendor skill copies.
- მათი წყარო `.ai/` დირექტორიაშია. შეცვალე canonical ფაილი და შემდეგ გაუშვი `npm run ai:sync`.
- `npm run ai:validate` ამოწმებს KAL-ს; ის არ ცვლის ფუნქციის browser/manual შემოწმებას.
- AI-ის მიერ შეცვლილი კოდი commit-მდე ყოველთვის გადახედე `git diff`-ით.

## მოკლე ფორმულა

AI-ის ცვლილება:

```text
AI მუშაობს → AI უშვებს sync/validate/tests → ადამიანი ამოწმებს diff-ს → commit → push
```

ადამიანის ხელით ცვლილება:

```text
შეცვალე → ai:sync → ai:validate → project test → შეამოწმე diff → commit → push
```
