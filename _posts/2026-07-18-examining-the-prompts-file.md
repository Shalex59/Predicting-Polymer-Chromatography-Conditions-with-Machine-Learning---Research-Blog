---
layout: post
title: "Examining-the-Prompts-File"
date: 2026-07-18
---
**The Prompts.py File**
Main topic of today's post is the prompts.py file in the package. It is the control room of the entire process and the guidelines outlined are to ensure the data mining only produces proper, research worthy data. After all, in a formal research environment, false data could destroy months of effort if not spotted early. A perfectly-formatted spreadsheet built on a bad prompt is still a bad spreadsheet. Worse than a messy one, honestly, because the formatting makes it look trustworthy whether or not it actually is. Every other file in the package is only as good as this one.

Another reason why 
**How each of the 16 points serves that goal**
 
1. **Pull every pair from tables, captions, and body text, not just the headline sentence.** Accuracy includes completeness — gathering all available information from the paper ensures as much useful information is captured as possible so.

2. **Skip ranges and "various"; never average or invent a midpoint.** A number that looks precise but was actually interpolated isn't accurate, it just looks accurate. Better to have no number than a fabricated one.

3. **A gradient solvent-composition change isn't a recipe.** Logging a two-part gradient as if it were one steady condition misrepresents what was actually tested, even if every individual number involved is real. We are looking for distinct and tangible data, not a range of values.

4. **Never infer adsorption vs. exclusion direction without data behind it.** A guessed direction that happens to be wrong is a worse outcome than an honest blank — it actively misinforms rather than just under-informing.

5. **Never infer base material, column chemistry, or solvent roles from a brand name or general convention.** Same idea as #4, aimed at metadata instead of the headline result. Being usually right isn't the same as being accurate about this specific paper.

6. **Don't read a value off a chart unless it's also printed as text.** A number eyeballed from a curve's position is an estimate; treating it as a stated fact misrepresents its own certainty. This point is, however, subject to change later on. We are still improving our code to read charts better, even if they are without accompanying text/captions.

7. **Include a paper's own self-flagged artifacts, marked invalid rather than dropped.** Deleting inconvenient data is inaccuracy by omission; keeping it without the flag is inaccuracy by overconfidence. The best move is including it with the caveat attached. After all, in such a gray zone where eliminating or including the data strictly as one or the other is not the best decision.

8. **Gradient elution is generally out of scope.** Same principle as #3 — don't represent a moving target as if it were a fixed one, as it is not a tangible, single result.

9. **Cross-check figure captions against body text and tables within the same paper; flag disagreements rather than picking one silently.** If the source itself is inconsistent, accurately transcribing only one side of that inconsistency is still a form of inaccuracy. If the paper disagrees with itself, the data row is not a confident pick.

10. **Watch for pore-size/particle-size swaps against standard naming convention.** Protects against transcribing a labeling mistake as if it were the real number.

11. **Every material claim needs an actual direct quote, not a paraphrase.** A paraphrase can drift from what the source actually said without notice. A quote is checkable against the PDF in seconds, which is what makes an accuracy claim verifiable. Furthermore, when troubleshooting the code, these direct quotes can help us track commercial LLM thinking and therefore determine what part of the code should be edited.

12. **Flag non-peer-reviewed sources explicitly, and watch for other gaps stacking on top.** Two sources can report the same figure with very different reliability behind it, and treating them as equivalent misrepresents that. This is a small condition as most papers are indeed peer reviewed. This concerns the credibility of the data, not its validity. 

13. **Flag likely cross-paper overlap, even without being able to verify it directly.** Self explanatory. To ensure minimal duplication, noting flags that appear can save time and effort during the checking process.

14. **Corresponding author only from an explicit marking, never the first-listed author by default.** An issue of credibility. Work must be correctly attributed to the right author, and that is one of the most important parts of mining data correctly. Giving credit to those who found the data is necessary.

15. **The same condition reported twice within one paper is one row, not two.** Otherwise a single finding restated in both a paragraph and a table looks like two independent confirmations of itself.

16. **For scanned or broken-text-layer pages, read the rendered image with an OCR instead of skipping the section.** Did not apply in our current state. This condition concerns older papers who were scanned and uploaded to websites, with their images being blurry/not rendered correctly.

**One seperate factor worth noting**
Not only are all quotes and factors worthy of cpnsideration included inside the notes column, any other flags with the data are included inside the column too. This serves to ensure the data is properly understood within the context in which it was mined.

**Why one at a time, and not directly uploading 5 at a time into the AI interface?**
Big question that needs to be addressed. Almost every one of those 16 rules exists to catch a specific way an LLM can be confidently wrong. THis is a big problem because we don't know where it may occur and would complicate the troubleshooting process. 

Batching a couple of these research papers together risks LLMs misattributing one paper's value to another, increasing the risk a inaccurate piece of data occurs. There is, in fact, formal research done on this. Liu et al, who studied GPT 3.5, 4, and Claude models found that performance followed a U shaped curve, meaning that information at the ends were given more attention. This means that not every paper in the batch is given 1/5 of the effort (we don't want that, we want each paper to be given the same consideration).
