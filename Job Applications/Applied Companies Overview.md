# Job Applications Dashboard

```dataviewjs
// Fetch all pages with a 'company' field in the folder "Job Applications/2025"
const pages = dv.pages('"Job Applications/2025"').where(p => p.company);

// Group the pages by company name
const grouped = pages.groupBy(p => p.company);

// Render the table with Company, Number of Jobs, and list of Applied Jobs
dv.table(
  ["Company", "Number of Jobs", "Applied Jobs"],
  grouped.map(group => [
    group.key,                    // Company name
    group.rows.length,            // Count of jobs applied for this company
    group.rows.map(p => p.job_position).join(", ") // List of job positions separated by commas
  ])
);
