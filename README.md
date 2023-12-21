# assign
import json
import requests

def fetch_and_store_json(url):
    try:
        response = requests.get(url)
        response.raise_for_status()  
        data = response.json()

        items = data.get('items', [])

        
        sorted_items = sorted(items, key=lambda x: x.get('popularity', 0), reverse=True)

       
        for item in sorted_items:
            title = item.get('title', 'N/A')
            price = item.get('price', 'N/A')
            print(f"Title: {title}, Price: {price}")

    except requests.exceptions.HTTPError as errh:
        print(f"HTTP Error: {errh}")
    except requests.exceptions.ConnectionError as errc:
        print(f"Error Connecting: {errc}")
    except requests.exceptions.Timeout as errt:
        print(f"Timeout Error: {errt}")
    except requests.exceptions.RequestException as err:
        print(f"Request Error: {err}")


json_url = 'https://s3.amazonaws.com/open-to-cors/assignment.json'
result=fetch_and_store_json(json_url)
if result :
  print(result)
