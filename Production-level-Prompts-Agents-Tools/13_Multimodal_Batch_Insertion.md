## Multimodal + Batch — Revision Card

- Multimodal inputs consume context before any text is read.
- Every image/PDF adds token cost at ingestion time, not just during reasoning.

- Image cost rule:
  - Claude views images in patches.
  - Approximate visual tokens = ceil(width / 28) × ceil(height / 28).
  - Large images are downscaled by model limits.
  - Check model-specific resolution/token limits before shipping.

- Practical image guidance:
  - Resize oversized images early.
  - Prefer URL or Files API for reused assets.
  - Base64 is fine for one-offs, but it adds payload overhead and cost.

- PDF handling:
  - Use document blocks, not image blocks.
  - Same source options: base64, URL, or Files API file_id.
  - Title/context are optional; cost still matters.

- Prompting for multimodal inputs:
  - Use structured prompts.
  - Specify how to handle ambiguity: overlap, depth, occlusion, partial visibility.
  - A vague prompt gives shallow answers.

- Batch API:
  - Best for hundreds/thousands of offline tasks.
  - Lower per-token cost; async; poll for results.
  - Latency can be long (up to ~24h), so not for interactive UX.

- Best fit:
  - Nightly classification jobs
  - Eval runs across many examples
  - Offline document extraction / labeling pipelines

- Bad fit:
  - Real-time user chat
  - Any feature where the user is waiting for a reply

- Failure modes to avoid:
  - Using batch in a user-facing flow
  - Ignoring image/PDF token cost before deployment

Quick checklist

- Estimate token cost of real production images/PDFs
- Resize before deploy if needed
- Prefer Files API/URLs for reusable assets
- Add explicit ambiguity-handling instructions
- Use Batch only for offline, non-interactive workloads

### Q&A (flashcards)

1. **Why are images expensive?**  
   They consume visual tokens before any prompt text is processed.

2. **What is the rough image formula?**  
   ceil(width / 28) × ceil(height / 28).

3. **When is base64 fine?**  
   One-off image use with no reuse.

4. **What is the PDF block type?**  
   document, not image.

5. **Why do multimodal prompts need structure?**  
   Images contain ambiguity that text prompts do not resolve on their own.

6. **When use Batch API?**  
   For high-volume offline pipelines and evals, not user-facing responses.

7. **What is the biggest risk?**  
   Underestimating context cost or choosing batch for interactive work.

8. **One-line rule?**  
   Measure multimodal token cost early, and reserve Batch for offline throughput, not waiting users.
