

```dataviewjs
const statusColors = {
    "Pending": "background-color: #FFD700; color: black; padding: 2px 6px; border-radius: 4px;",
    "Interview": "background-color: #1E90FF; color: white; padding: 2px 6px; border-radius: 4px;",
    "Accepted": "background-color: #228B22; color: white; padding: 2px 6px; border-radius: 4px;",
    "Rejected": "background-color: #B22222; color: white; padding: 2px 6px; border-radius: 4px;"
};

dv.table(
    ["Position Applied", "Applied", "Answered", "Response Time (days)", "Company", "Status", "Cover Letter", "Resume", "File"],
    dv.pages('"Job Applications/2025"')
      .sort(p => p.application_date, 'desc')
      .map(p => [
        p.job_position ?? "",
        p.application_date ?? "",
        p.answer_date ?? "",
        p.answer_date && p.application_date ? ((dv.date(p.answer_date) - dv.date(p.application_date)) / (1000*60*60*24)).toFixed(0) + " days" : "—",
        p.company ?? "",
        p.status ? `<span style="${statusColors[p.status] || ''}">${p.status}</span>` : "",
        p.cover_letter ? dv.fileLink(p.cover_letter) : "",
        p.resume_used ? dv.fileLink(p.resume_used) : "",
        p.file.link ?? ""
      ])
);
