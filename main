import json,httpx,random,threading

def get_username_spoko_ok(username):
    headers = {'Client-Id': 'kimne78kx3ncx6brgo4mv6wki5h1ko'}
    data = {
        "operationName": "WatchTrackQuery",
        "variables": {
            "channelLogin": username,
            "videoID": None,
            "hasVideoID": False
        },
        "extensions": {
            "persistedQuery": {
                "version": 1,
                "sha256Hash": "38bbbbd9ae2e0150f335e208b05cf09978e542b464a78c2d4952673cd02ea42b"
            }
        }
    }

    try:
        response = httpx.post('https://gql.twitch.tv/gql', headers=headers, json=[data])
        user_data = response.json()[0]['data']['user']
        return user_data['id']
    except (KeyError, TypeError):
        return None
    
def Follow(target_id):
    tokens_data = open('integrity.txt', 'r').read().splitlines()
    data = json.loads(random.choice(tokens_data))
    authorization = data['access']
    integrity = data['integrity']['token']
    proxy = "http://" + data['integrity']['proxy']
    device_id = data['integrity']['data']['X-Device-ID']
    client_id = data['integrity']['data']['Client-ID']
    user_agent = data['integrity']['data']['User-Agent']

    headers = {
        'Accept': '*/*',
        'Accept-Language': 'pl-PL',
        'Authorization': 'OAuth ' + authorization,
        'Client-Id': client_id,
        'Client-Integrity': integrity,
        'Client-Session-Id': '80464b838e2668b7',
        'Client-Version': '2f39f041-c104-4960-8a91-eeda943d18ec',
        'Connection': 'keep-alive',
        'Content-Type': 'text/plain;charset=UTF-8',
        'Origin': 'https://www.twitch.tv',
        'Referer': 'https://www.twitch.tv/',
        'Sec-Fetch-Dest': 'empty',
        'Sec-Fetch-Mode': 'cors',
        'Sec-Fetch-Site': 'same-site',
        'Sec-GPC': '1',
        'User-Agent': user_agent,
        'X-Device-Id': device_id,
        'sec-ch-ua': '"Chromium";v="116", "Not)A;Brand";v="24", "Brave";v="116"',
        'sec-ch-ua-mobile': '?0',
        'sec-ch-ua-platform': '"Windows"',
    }

    data = {
        "operationName": "FollowButton_FollowUser",
        "variables": {
            "input": {
                "disableNotifications": False,
                "targetID": target_id
            }
        },
        "extensions": {
            "persistedQuery": {
                "version": 1,
                "sha256Hash": "800e7346bdf7e5278a3c1d3f21b2b56e2639928f86815677a7126b093b2fdd08"
            }
        }
    }

    response = httpx.post('https://gql.twitch.tv/gql', headers=headers, json=[data], proxies=proxy, timeout=5)
    print(response.text)

def threadxpp(target_id, num_follows):
    for _ in range(num_follows):
        Follow(target_id)

def gut():
    username = input("Enter Username: ")
    num_follows = int(input("Enter amount follows: "))

    target_id = get_username_spoko_ok(username)

    if target_id is not None:
        threads = []

        for _ in range(num_follows):
            thread = threading.Thread(target=threadxpp, args=(target_id, 1))
            threads.append(thread)
            thread.start()

        for thread in threads:
            thread.join()
    else:
        print(f"Invalid: {username}")

if __name__ == "__main__":
    gut()
