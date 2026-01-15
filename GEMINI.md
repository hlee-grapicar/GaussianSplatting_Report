# GEMINI Context & Standards

## Documentation Standard
When creating new reports or READMEs, adhere to the following structure to maintain consistency:

*   **Header:**
    *   H1 Title.
    *   (Optional) Centered Representative Image (Figure 0).
*   **Abstract:**
    *   High-level summary using bullet points: **Objective**, **Process**, **Key Finding**.
*   **Introduction:**
    *   Bullet points defining **Purpose**, **Scope**, and **Focus**.
*   **System Specifications:**
    *   Standard Markdown Table defining CPU, RAM, GPU, VRAM.
*   **Methodology:**
    *   Broken down by stage (e.g., Data Acquisition, Preprocessing).
    *   Use bullet points.
    *   **Images:** Use standard HTML tags for centering and captioning:
        ```html
        <p align="center">
          <img src="filename.png" alt="Alt Text" width="600"/>
          <br>
          <em>Figure X: Caption.</em>
        </p>
        ```
    *   **Side-by-Side Comparisons:** When presenting comparison images, the "Failure/Negative" case should be on the **Left** and the "Success/Positive" case should be on the **Right**.
*   **Results & Conclusion:**
    *   Summary of outcomes and recommendations.
