
1. Official Power BI Service (Cloud)

In the cloud, the limits apply to the compressed in-memory size of a single dataset. Because Power BI compresses data heavily, your 10M rows × 100 columns will likely take up 1 GB to 2 GB of space.
• Power BI Pro: 1 GB maximum per dataset.
	• Warning: Your 100 columns might put you dangerously close to or over this limit as the 50k daily rows pile up.
• Power BI Premium Per User (PPU): 100 GB maximum per dataset.
• Power BI Premium Capacity / Fabric (F-SKUs): 25 GB to 400 GB+ per dataset (depending on the SKU tier your company buys).
Note: The total overall storage workspace limit across all reports is 10 GB for Pro and up to 100 TB for Premium.

🖥️ 2. Power BI Report Server (On-Premises)

If your company is hosting reports on their own local server, the limits are governed by file size rather than cloud licensing capacity:
• Maximum File Size: 2 GB maximum per .pbix file.
	• Warning: Because Incremental Refresh does not work here, the server must pull all 10M + 50k rows every day. If the compressed size of that full history ever crosses 2 GB, the file will fail to upload or refresh entirely.
• Server Hardware Limits: There is no software cap on total workspace storage; it is limited entirely by the hard drive space and RAM available on your company's physical server hardware.

💡 Summary for your Architecture

If your company uses Power BI Pro or On-Premises Report Server, you are at high risk of crashing into the 1 GB / 2 GB limits due to your massive 100-column width. If you use Premium/Fabric, you have absolutely nothing to worry about.
Do you know which license or environment (Pro, Premium, or On-Premises Server) your team is currently tracking against? If you are on Pro or On-Premises, I can show you how to check your exact current dataset size in Power BI Desktop before publishing.
Try without personalization


[ Power BI Desktop ] ──> Define Parameters & Policy ──> Pulls ALL 10M rows locally (once)
          │
          ▼ (Publish)
[ Power BI Service ] ──> Creates isolated partitions ──> Daily refreshes read ONLY the 50k rows
