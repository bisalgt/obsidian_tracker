# 📚 Learning Progress Dashboard

```dataviewjs
const statusColors = {
    "Pending": "background-color: #FFD700; color: black; padding: 2px 6px; border-radius: 4px;",
    "Started": "background-color: #1E90FF; color: white; padding: 2px 6px; border-radius: 4px;",
    "Completed": "background-color: #228B22; color: white; padding: 2px 6px; border-radius: 4px;",
    "Stopped": "background-color: #B22222; color: white; padding: 2px 6px; border-radius: 4px;"
};

// Fetch all notes that have course_title in frontmatter
const pages = dv.pages('"Learning"')
    .where(p => p.course_title);

// Build table with course info including career_path and colored status label
dv.table(
    ["Course Title", "Career Path", "Start Date", "Anticipated Completion", "Status", "Skills", "Website", "Certificate", "Source", "Cost", "File"],
    pages
      .sort(p => p.start_date, 'asc')
      .map(p => [
        p.course_title ?? "",
        p.career_path ?? "",
        p.start_date ? dv.date(p.start_date).toFormat("yyyy-MM-dd") : "",
        p.anticipated_complete_date ? dv.date(p.anticipated_complete_date).toFormat("yyyy-MM-dd") : "",
        p.status ? `<span style="${statusColors[p.status] || ''}">${p.status}</span>` : "",
        p.skills ? (Array.isArray(p.skills) ? p.skills.join(", ") : p.skills) : "",
        p.website ?? "",
        p.certificate ?? "",
        p.source ?? "",
        p.cost ?? "",
        p.file.link
      ])
);
