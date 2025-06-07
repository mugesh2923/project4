# project4
# Website Integrity & Uptime Monitoring Tool (Python Automation)
  This tool helps to check if websites are online (UP) or offline (DOWN). It also verifies if a specific keyword is present on the website to make sure the website content has not been changed or hacked.
# Technologies Used:
Python – Programming language used to write the tool

Requests library – To send HTTP requests to websites and get their content

File handling – To save the check results into a text file

Basic string operations – To search for keywords inside website content

# code
      import requests

      # 1. Get multiple websites and keyword from user
      websites = input("Enter websites (comma separated, like google.com, facebook.com): ")
      keyword = input("Enter keyword to search in websites: ")

     # 2. Split websites into a list
     website_list = websites.split(",")

     # 3. Set a simple output file name
     file_name = "website_result.txt"

     # 4. Open file to save results
     output_file = open(file_name, "w")

     # 5. Loop through each website
     for site in website_list:
          site = site.strip()  # Remove extra space

             if not site.startswith("http"):
                 site = "https://" + site  # Add https if missing

            try:
        response = requests.get(site, timeout=5)

        if response.status_code == 200:
            if keyword in response.text:
                result = f"✅ {site} is UP and content is OK"
            else:
                result = f"⚠️ {site} is UP but keyword not found (Content changed)"
        else:
            result = f"❌ {site} is reachable but returned status code {response.status_code}"
    except:
        result = f"❌ {site} is DOWN or not reachable"

    # Show in terminal and save in file
    print(result)
    output_file.write(result + "\n")

# 6. Close the file
output_file.close()

print("\n📁 All results saved to website_result.txt")


