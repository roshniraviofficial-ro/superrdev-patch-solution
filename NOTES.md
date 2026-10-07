# Patch Notes

## Summary of Changes
- **Removed Artificial Latency:** Removed `Thread.sleep` and complexity scoring logic in `TaskController.java` (`searchTasks` endpoint) to eliminate artificial API delays.
- **Fixed Pagination Slicing:** Corrected the `subList` pagination boundary calculations in `TaskController.java` to ensure a consistent page size of 10 items.
- **Repository Clean-Up:** Removed redundant '@Repository`annotation and unused imports in `TaskRepository.java`.

## What was Not Changed & Why
- **In-Memory Slicing:** Kept the existing `allResults.subList(...)` pagination approach rather than refactoring to SQL-Level `Pageable` database queries. This keeps the diff minimal and focused while fully resolving the visible bug.

## Biggest Remaining Risk
- **Scalability with Large Datasets:** Fetching all task records from the database before slicing in memory will lead to performance bottlenecks if the database grows significantly. Future work should implement Spring Data JPA `Pageable` queries at the database layer.

## Tools & AI Used
- Used Gemini for codebase review, diagnosing the artificial delay logic in `TaskController.java`, and verifying Java 17 compatibility.