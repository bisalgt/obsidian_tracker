

```dataview
table job_position as "Position Applied", application_date as "Applied", answer_date as "Answered", 
(date(answer_date) - date(application_date)) as "Response Time (days)", 
company as "Company", status as "Status"
from "Job Applications/2025"
where contains(file.name, "")
sort application_date desc