# Public GitHub repository cleanup audit

Account: [Arshad9999](https://github.com/Arshad9999). Audit date: 27 October 2026.

## Publication status

The initial 30-repository audit and cleanup are published: 23 repositories received routine documentation/provenance/ignore commits on their default branches, and seven pull requests contain the four web app updates, two Python check/fix updates, and profile rewrite. Descriptions were updated for all 21 non-fork repositories, and 14 follow-up issues were created. GitHub Actions passed for all six repositories receiving new test workflows. The pull requests remain open for review.

The original integration rejected writes with HTTP 403. The owner completed GitHub CLI browser authorization as Arshad9999, and publishing succeeded through that login. No additional GitHub write permission is currently needed for these operations.

### Pull requests

- [arshad-finance-blog-01](https://github.com/Arshad9999/arshad-finance-blog-01/pull/1)
- [Arshad9999](https://github.com/Arshad9999/Arshad9999/pull/2)
- [c-foundations-2025](https://github.com/Arshad9999/c-foundations-2025/pull/1)
- [google-cohort2-arcade25](https://github.com/Arshad9999/google-cohort2-arcade25/pull/1)
- [Machine-Learning](https://github.com/Arshad9999/Machine-Learning/pull/3)
- [pattern_recognition](https://github.com/Arshad9999/pattern_recognition/pull/1)
- [PythonPlayground](https://github.com/Arshad9999/PythonPlayground/pull/1)

[Central cleanup tracker](https://github.com/Arshad9999/Arshad9999/issues/3).

## Findings

- 30 repositories inspected; 9 are GitHub forks and 21 are marked non-fork.
- 15 have a detected repository-wide license; 15 do not. No license was invented or replaced.
- Four newer React/TypeScript applications had generic Lovable READMEs. Their histories include generated-code commits.
- `6Companies30Days` is marked non-fork but its imported history credits Vortex-21/vortex-21. Non-fork status is insufficient for an original-work claim.
- `shopifyMall` contains third-party dependency directories at the root, without a root application manifest or entry point. Application recovery is needed.
- `InternPeJavaDevelopment` contains only a README and license; `Arshad9999.github.io` contains only a README at the audited revision.
- `TicTacToe` is an Android application, despite its generic Java-oriented README.

## Validation and prepared fixes

| Project | Before | Prepared result |
| --- | --- | --- |
| arshad-finance-blog-01 | 23 audit findings; build passed; lint failed | Clean build, lint and 2 route tests pass; 0 npm audit findings |
| c-foundations-2025 | 23 audit findings; build passed; lint failed | Clean build, lint and 2 route tests pass; 0 npm audit findings |
| google-cohort2-arcade25 | 26 audit findings; build passed; lint failed | Clean build, lint and 2 route tests pass; 0 npm audit findings |
| pattern_recognition | 23 audit findings; inconsistent lockfile prevented npm ci | Clean build, lint and 2 route tests pass; 0 npm audit findings |

The pattern_recognition baseline audit used an incomplete lockfile, so its before/after counts are not a like-for-like comparison of the entire resolved graph. `npm audit` is a point-in-time advisory check, not proof of application security.

The four app patches update Vite, its React plugin, React Router, Vitest, and lint tooling; repair the pattern_recognition lockfile; remove five unused direct dependencies per app; add two real route tests per app; and configure CI and Dependabot. The unused direct dependencies are `@hookform/resolvers`, `date-fns`, `zod`, `lovable-tagger`, and `@tailwindcss/typography`. Transitive packages may still be needed by other dependencies. Runtime requirements are documented as Node 24, with compatible Node 22.13+ also allowed. Validation used Node 24.22.1. Existing non-fatal Fast Refresh warnings remain.

The Machine-Learning patch repairs eight syntax-invalid Python files and implements the missing two-layer forward_propagation function. Four regression tests pass, including matrix shape/error cases and syntax checks. It adds requirements and CI, but full dataset-dependent training has not been run. Four PythonPlayground behavior tests pass and CI is prepared. Both Java exercises in LetsLearnGit compile with JDK 20.0.1.

All 30 repositories have prepared ignore-file improvements. Non-fork project READMEs were made repository-specific; the profile has a conservative draft and a complete portfolio directory. Nine forks receive a separate FORK_NOTES.md, preserving their upstream README and license. Existing .DS_Store files are removed in the patches; no application dependency snapshot or source tree was bulk deleted. Four app READMEs include architecture diagrams; JaalNetra references an existing screenshot and a static architecture diagram.

## Secret scanning

Gitleaks 8.30.1, downloaded from its official release and checksum-verified, scanned all 30 local Git histories with `--log-opts=--all` and full redaction. The clone was not shallow. Coverage includes fetched branches and reachable history, not deleted Git objects or remote-only unreachable references. No candidate was tested against a live service and no credential values are included in this report.

- `buyitup`: historical next.config.js includes a Stripe **test** secret-key pattern and a Cloudinary secret candidate. The same configuration includes DB_URI and NEXTAUTH_SECRET fields that require credential-owner review. That file is absent on the current default branch but remains in history. The actual credential owner must revoke/rotate real values; fork ownership does not confer ownership of the upstream service accounts.
- `netflix2.0`: current source has a movie API key candidate and Firebase web configuration. Firebase client API keys are not automatically private credentials; restrictions, service permissions and Firebase rules need review. Do not assume a client-side .env file makes bundled values secret.
- `AI-For-Beginners`: a historical notebook contains a NewsAPI credential candidate, inherited from upstream.
- MIT-course fork: matches include encoded notebook images and historical documentation tokens; these require triage rather than automatic credential rotation claims.
- `shopifyMall`: scanner matches are in vendored third-party documentation, fixtures, compiled library code, and example keys. These were not classified as confirmed active user credentials.

No credentials have been rotated. History was not rewritten. New secret-bearing examples were not introduced. The four maintained web apps currently require no environment variables, so they do not receive unnecessary placeholder .env files. Service-specific safe examples and config migration remain pending for legacy apps.

## Remaining dependency work

| Project | Audit findings | Critical | Scope |
| --- | ---: | ---: | --- |
| buyitup | 76 | 6 | Existing lockfile; no forced framework migration applied |
| netflix2.0 | 73 | 5 | Existing lockfile; no forced framework migration applied |
| vercel-readme-stats | 32 | 2 | Existing lockfile; no forced framework migration applied |

Ruby/Chef, Android/Gradle, Python environment and notebook dependencies have not received complete ecosystem vulnerability audits. The npm scan does not cover those ecosystems or shopifyMall’s unstructured dependency snapshot.

## Demo checks

HTTP 200 verifies reachability only. It does not establish ownership, full functionality, or that a deployment matches the audited commit.

| Repository/reference | URL | Result |
| --- | --- | --- |
| arshad-finance-blog-01 | [https://arshad-finance-blog-01.vercel.app](https://arshad-finance-blog-01.vercel.app) | 200; WealthWise India - Master Your Financial Future |
| c-foundations-2025 | [https://c-foundations-2025.vercel.app](https://c-foundations-2025.vercel.app) | 200; Lovable App |
| google-cohort2-arcade25 | [https://google-cohort2-arcade25-facilitator.vercel.app](https://google-cohort2-arcade25-facilitator.vercel.app) | 200; Google Arcade 2025 |
| Arshad9999.github.io | [https://arshad9999.github.io/](https://arshad9999.github.io/) | 200; Arshad9999.github.io |
| JaalNetra | [https://goodybla001.github.io/level1project/](https://goodybla001.github.io/level1project/) | 200; 1st Website Link! | level1project |

The JaalNetra README’s former link points to a different account’s Pages site and is not represented as a verified deployment of Arshad’s repository. No deployed site is claimed for pattern_recognition. Other links embedded in large curricula, course notebooks and external badges have not all been exhaustively crawled.

## All-repository inventory

Each link identifies the audited default-branch revision. Author counts are metadata evidence only; they do not prove authorship or independently implemented features.

| Repository | Purpose/category | Fork/upstream | License | Tracked files |
| --- | --- | --- | --- | ---: |
| [10-Image-Classification-using-CNN](https://github.com/Arshad9999/10-Image-Classification-using-CNN/tree/b3121e5cffe944341634c118a322a86de960871b) | A learning notebook exploring convolutional neural networks with TensorFlow and the ten-class CIFAR-10 image dataset. | Non-fork | Apache-2.0 | 7 |
| [6Companies30Days](https://github.com/Arshad9999/6Companies30Days/tree/9da4f33d577409aa212a3de8f1194d3ab4836ad8) | A collection of C++ interview practice solutions and problem notes for the #6Companies30Days challenge. | Non-fork | Apache-2.0 | 35 |
| [AI-Adventures-Diving-Into-Deep-Learning](https://github.com/Arshad9999/AI-Adventures-Diving-Into-Deep-Learning/tree/3d7b51132876ffc91f1b0f0bd1383d34da030746) | MIT 6.S191 deep-learning course notebooks and lab materials. Training was not executed; notebooks need their documented datasets and compute resources. | MITDeepLearning/introtodeeplearning | MIT | 70 |
| [AI-For-Beginners](https://github.com/Arshad9999/AI-For-Beginners/tree/32a0d200e289a7ffde4ab39e3a2a164aa7b92f83) | Microsoft’s AI curriculum, including notebooks and lesson material. This fork is a learning resource; no complete curriculum execution was attempted. | microsoft/AI-For-Beginners | MIT | 324 |
| [arshad-finance-blog-01](https://github.com/Arshad9999/arshad-finance-blog-01/tree/2b6849590f081ed857f79ec79c1e3a5f8755a3b8) | A React and TypeScript educational finance website with trading basics, tax guides, career resources, investment topics, and a blog page. | Non-fork | Not detected | 97 |
| [Arshad9999](https://github.com/Arshad9999/Arshad9999/tree/4b50be51908b525a4670ee8f4b7e92bab3bca11f) | The README displayed on the Arshad9999 GitHub profile. | Non-fork | Not detected | 7 |
| [Arshad9999.github.io](https://github.com/Arshad9999/Arshad9999.github.io/tree/abb7c038e2f07c190bab967cb99b4e2f18beb18f) | A starter GitHub Pages repository. The current source contains a README rather than a custom portfolio application. | Non-fork | Not detected | 2 |
| [aws](https://github.com/Arshad9999/aws/tree/b83aadcf05cece87c940ef8fcee396877d5351be) | The Sous Chefs AWS cookbook, implemented in Ruby/Chef. Its integration tests need a Chef environment and may need cloud credentials; cloud provisioning was not run. | sous-chefs/aws | Apache-2.0 | 89 |
| [BigDataAnalytics](https://github.com/Arshad9999/BigDataAnalytics/tree/81662acf8755b594bb832521ee840865607ad07c) | Markdown study notes covering big data analytics, data mining, Hadoop, and distributed data processing. | Non-fork | Not detected | 2 |
| [buyitup](https://github.com/Arshad9999/buyitup/tree/ba8148b2f9773e718f87023cdf811a093c1d8b52) | A Create React App e-commerce frontend on the default branch. Historical commits contain a different Next.js application; the historical credentials are not proof that a backend exists on this branch. | ghulamabbas2/buyitnow | Not detected | 45 |
| [c-foundations-2025](https://github.com/Arshad9999/c-foundations-2025/tree/874863cbb867233b3e5e634397a13bb5abdf9124) | A React and TypeScript learning website with C programming topics, questions, and a lab-program page. The repository contains the website, rather than a standalone C application. | Non-fork | Not detected | 90 |
| [EleoXDA](https://github.com/Arshad9999/EleoXDA/tree/42758614416c2802b67fe9b57cb74a4bfd8e2d2e) | Another developer’s profile README and profile-visualization workflows. Its biography describes the upstream owner, not Arshad. | EleoXDA/EleoXDA | Not detected | 9 |
| [google-cloud-arcade-2023](https://github.com/Arshad9999/google-cloud-arcade-2023/tree/6f8f755c348704120eec4a7be328bfeb701c4593) | Study notes and challenge material collected for the 2023 Google Cloud Arcade seasons. | Non-fork | Not detected | 6 |
| [google-cohort2-arcade25](https://github.com/Arshad9999/google-cohort2-arcade25/tree/123916d6cc3546af3a12cab41de87f5844e81c9f) | A React and TypeScript community information site with a calculator route and browser-local profile storage for the 2025 Arcade cohort. | Non-fork | Not detected | 83 |
| [HSSMC-for-Engineers](https://github.com/Arshad9999/HSSMC-for-Engineers/tree/6df36a84e815c8fe9b74305d7099d78f4fb837f1) | Module-based study notes on engineering economics, Indian history, law, and sociology. | Non-fork | MIT | 22 |
| [InternPeJavaDevelopment](https://github.com/Arshad9999/InternPeJavaDevelopment/tree/40ae4a3ae0593fe0032945cc84f6a0e9b202533b) | A Java development repository scaffold. The current revision contains a README and MIT license; no Java implementation is checked in. | Non-fork | MIT | 3 |
| [IoT-InternetofThings](https://github.com/Arshad9999/IoT-InternetofThings/tree/0bc398d9b0e7865d1f318e2d5a7b86c772bb1da5) | Networking lab notes describing topologies and Cisco Packet Tracer exercises. | Non-fork | Not detected | 7 |
| [JaalNetra](https://github.com/Arshad9999/JaalNetra/tree/71bb20fb132f0ef8fef1fe9d4dd4c866d8402a9c) | A static HTML, CSS, and JavaScript project website with home, demo, download, documentation, help, and contact pages. Its branding refers to network analysis; the repository does not contain a working packet-capture backend. | Non-fork | Not detected | 30 |
| [LetsLearnGit](https://github.com/Arshad9999/LetsLearnGit/tree/fa892e87d5c4e64d5590fbc060458b941a0d7c0b) | A Git practice repository that also contains two Java exercises. | Non-fork | Not detected | 4 |
| [Machine-Learning](https://github.com/Arshad9999/Machine-Learning/tree/84a28f5cb995d3a01225d0401229bf033e68e987) | Python lab exercises covering matrix operations, plotting, regression, classification, gradient descent, clustering, and neural-network forward propagation. | Non-fork | Apache-2.0 | 24 |
| [netflix2.0](https://github.com/Arshad9999/netflix2.0/tree/6e46c014b2c560c92dd873a129775b4aae2e18aa) | A Create React App/Redux movie-browsing frontend. It references Firebase and a movie API, but the manifest omits packages imported by the source. Runtime and service configuration need repair. | DevDuo2023/netflix2.0 | Apache-2.0 | 42 |
| [OpenGL-Vth](https://github.com/Arshad9999/OpenGL-Vth/tree/0707472ddc75e25f6d9d503eb8cec0fca6e184b5) | Fifteen C++ OpenGL/FreeGLUT lab exercises covering lines, letters, shapes, animation, and 3D objects. | Non-fork | MIT | 18 |
| [pattern_recognition](https://github.com/Arshad9999/pattern_recognition/tree/4ca5ba618cf59fbc12ecedd8b53dd08683d765bd) | A React and TypeScript educational website covering pattern recognition paradigms, classifiers, clustering, dimensionality reduction, and a practical assignment page. | Non-fork | Not detected | 92 |
| [Python-Deep-Learning](https://github.com/Arshad9999/Python-Deep-Learning/tree/861c19b544f5f438e8eb05566e7e1054d505d81e) | Learning notes and partial Python implementations for introductory neural-network lab exercises. Some lab directories contain notes only, and LAB 03/code.py is empty. | Non-fork | Apache-2.0 | 15 |
| [Python-DSA](https://github.com/Arshad9999/Python-DSA/tree/5746d13c29d0b6b5d8051d9bde2aadde2a4ee4e5) | A community collection of Python data-structure and algorithm exercises. These are individual learning examples rather than a packaged service. | BeeBombshell/Python-DSA | MIT | 69 |
| [PythonPlayground](https://github.com/Arshad9999/PythonPlayground/tree/b1cf89b7b0805373856627651b909f05dd7883f2) | Small Python exercises for Armstrong numbers, factorials, Fibonacci sequences, prime numbers, and a notebook of printed patterns. | Non-fork | Apache-2.0 | 8 |
| [shopifyMall](https://github.com/Arshad9999/shopifyMall/tree/4ac24bc0317913e54fabe0d031af8f8c6fd9f1d1) | The current tree consists primarily of third-party dependency package directories. There is no root application package.json, lockfile, or identifiable application entry point, so this revision cannot be treated as a runnable storefront. | Non-fork | Not detected | 16904 |
| [TicTacToe](https://github.com/Arshad9999/TicTacToe/tree/b036ef24d134bbd438bb93819866cfe2f0be2727) | An Android Java tic-tac-toe application with Gradle and Android resource files. Building requires a compatible Android SDK/Gradle/JDK setup; it is not a plain desktop Java application. | Mohd-Farhan/TicTacToe | Apache-2.0 | 56 |
| [University-Notes](https://github.com/Arshad9999/University-Notes/tree/3fcc8af243a970f0bd671badd0ce5e6f8b86d0cd) | A small notes repository containing workshop-practices material. | Non-fork | Not detected | 2 |
| [vercel-readme-stats](https://github.com/Arshad9999/vercel-readme-stats/tree/9eb0c3cbb40d551b93536c45100994d4c83b8c04) | An upstream GitHub Readme Stats serverless service. API endpoints may need a GitHub token; no real token was supplied or used for service calls. | anuraghazra/github-readme-stats | MIT | 97 |

## Runtime limits

Full CNN or curriculum training was not run. Windows/FreeGLUT programs need a suitable graphical toolchain; the Android application needs Android SDK/Gradle; Chef infrastructure tests need their own environment and possibly cloud credentials. No cloud resources were provisioned. Partial deep-learning lab methods have unresolved imports/data examples. JaalNetra references missing local files, including home.js and documentation.css, and has no packet-capture backend in this tree. The 2025 Arcade site has a past countdown, prototype calculator behavior, and profile persistence that ignores the Remember Me choice. These remain explicit follow-up tasks.

## Tracker status

| # | Task | Status |
| --- | --- | --- |
| 1 | Inspect actual repository purpose | Audit complete for 30 repositories |
| 2 | Check forks, owners, licenses, contribution history | Audit complete; authorship caveats recorded |
| 3 | Identify placeholder READMEs and missing setup | Audit complete; documentation prepared |
| 4 | Check runtime and demos | Partial; platform/dataset limits above |
| 5 | Search history for credentials | Scan complete; candidate triage and owner actions remain |
| 6 | Ignore files and environment examples | Ignores prepared; legacy service config migration remains |
| 7 | Rotate exposed secrets | Requires credential owners and issuing services |
| 8 | Dependencies and unused packages | Four app fixes verified; legacy and other ecosystems remain |
| 9 | README sections and descriptions | 23 direct cleanup commits; remaining READMEs in PRs; 21 descriptions updated |
| 10 | Screenshots and architecture | Relevant diagrams and an existing screenshot reference prepared |
| 11 | Tests and GitHub Actions | Six repositories have prepared checks; broader platform checks remain |
| 12 | Create follow-up issues | 14 follow-up issues created |
| 13 | Pin 4–6 projects | Unchanged: browser capture failed while opening the selector; choose pins through the account UI |
| 14 | Update profile and education | Conservative profile draft prepared; current personal facts missing |
| 15 | Separate learning and portfolio projects | Complete directory prepared |
| 16 | Verified demos and contributions | Reachability and history evidence documented; ownership/feature caveats remain |

## Manual actions needed

1. Review the seven open pull requests. CLI publishing access is already authorized; no password or token needs to be pasted into chat.
2. Credential owners must review and rotate historical service credentials where real.
3. Supply current education/employment facts before they can be added accurately to the profile.
4. Choose license terms for unlicensed projects after confirming rights; no license is assigned automatically.
5. Review proposed portfolio choices and pin only projects whose limitations you are comfortable presenting.

## Safety of the prepared changes

The changes and pull requests above were published successfully. No repository was deleted, archived, renamed or made public/private. No license was replaced and no history was rewritten. No deployment workflow was manually dispatched; existing push-triggered workflows can run when commits are published.

## GitHub Actions evidence

- [arshad-finance-blog-01 — Application checks](https://github.com/Arshad9999/arshad-finance-blog-01/actions/runs/40446080952): success.
- [c-foundations-2025 — Application checks](https://github.com/Arshad9999/c-foundations-2025/actions/runs/40446114947): success.
- [google-cohort2-arcade25 — Application checks](https://github.com/Arshad9999/google-cohort2-arcade25/actions/runs/40446132104): success.
- [Machine-Learning — Python lab checks](https://github.com/Arshad9999/Machine-Learning/actions/runs/40446159515): success.
- [pattern_recognition — Application checks](https://github.com/Arshad9999/pattern_recognition/actions/runs/40446178505): success.
- [PythonPlayground — Python exercises](https://github.com/Arshad9999/PythonPlayground/actions/runs/40446196542): success.

## Follow-up issues

- [Arshad9999: Track repository cleanup and confirm profile facts](https://github.com/Arshad9999/Arshad9999/issues/3)
- [shopifyMall: Recover application source and manifest before treating this as a storefront](https://github.com/Arshad9999/shopifyMall/issues/1)
- [buyitup: Plan migration of the legacy Create React App dependency tree](https://github.com/Arshad9999/buyitup/issues/1)
- [netflix2.0: Repair missing dependencies and migrate the legacy web build](https://github.com/Arshad9999/netflix2.0/issues/1)
- [vercel-readme-stats: Review upstream updates and vulnerable serverless dependencies](https://github.com/Arshad9999/vercel-readme-stats/issues/1)
- [google-cohort2-arcade25: Resolve prototype calculator and profile-persistence behavior](https://github.com/Arshad9999/google-cohort2-arcade25/issues/2)
- [JaalNetra: Restore missing static assets and distinguish website from backend capabilities](https://github.com/Arshad9999/JaalNetra/issues/3)
- [Python-Deep-Learning: Complete lab imports, input examples and executable training checks](https://github.com/Arshad9999/Python-Deep-Learning/issues/1)
- [Machine-Learning: Document dataset sources and validate remaining training labs](https://github.com/Arshad9999/Machine-Learning/issues/4)
- [6Companies30Days: Verify attribution and original contribution claims](https://github.com/Arshad9999/6Companies30Days/issues/1)
- [TicTacToe: Document and validate the Android build environment](https://github.com/Arshad9999/TicTacToe/issues/1)
- [OpenGL-Vth: Validate the graphics labs on their supported toolchain](https://github.com/Arshad9999/OpenGL-Vth/issues/2)
- [InternPeJavaDevelopment: Add the intended Java implementation or keep this explicitly a scaffold](https://github.com/Arshad9999/InternPeJavaDevelopment/issues/1)
- [Arshad9999.github.io: Confirm the intended portfolio site source and deployment](https://github.com/Arshad9999/Arshad9999.github.io/issues/1)

## Suggested profile pins

The browser-control service failed while opening the pin selector, so no pins were changed. Suggested non-fork repositories to feature after reviewing their cleanup PRs:

- [WealthWise India](https://github.com/Arshad9999/arshad-finance-blog-01)
- [C Foundations](https://github.com/Arshad9999/c-foundations-2025)
- [Pattern Recognition](https://github.com/Arshad9999/pattern_recognition)
- [PythonPlayground](https://github.com/Arshad9999/PythonPlayground)

The first three include generated scaffolding, as documented in their READMEs; the last is a collection of checked small learning exercises. The open PRs preserve the review step for code upgrades.
