import argparse
import requests

dogApiEndpoint = "https://dog.ceo/api/breeds/list/all"
response = requests.get(url=dogApiEndpoint)
response.raise_for_status()
dogData = response.json()["message"]

parser = argparse.ArgumentParser(description="Find dog breed / Sub breed")
parser.add_argument('--breed', type=str.lower,
                    help='enter name of breed (Mandatory)', required=True)
parser.add_argument('--list', help='If the breed has sub-breeds, list the sub-breeds',
                    required=False, action='store_true')
parser.add_argument('--count', help='Count the number of sub breeds',
                    required=False, action='store_true')
parser.add_argument('--image', help='Download a random picture of a dog breed',
                    required=False, action='store_true')
args = parser.parse_args()

if args.breed in dogData:
    if args.list:
        if len(dogData[args.breed]) > 0:
            print(f"sub-breeds are: {dogData[args.breed]}")
        else:
            print(f"No sub-breeds")
    if args.count:
        if len(dogData[args.breed]) > 0:
            print(f"number of sub-breeds: {len(dogData[args.breed])}")
        else:
            print(f"No sub-breeds")
    if args.image:
        dogApi_download = f"https://dog.ceo/api/breed/{args.breed}/images/random"
        download_response = requests.get(
            url=dogApi_download, allow_redirects=True)
        download_response.raise_for_status()
        new_path_download = download_response.json()["message"]
        dnld = requests.get(url=new_path_download)
        dnld.raise_for_status()
        with open("{}".format(new_path_download.split("/")[-1]), "wb") as dnld_dog_pic:
            dnld_dog_pic.write(dnld.content)
else:
    print("There is not such breed, or misspeld the breed")
    print("Here are the name of breeds: ")
    for key in dogData:
        print(key, end=" , ")
