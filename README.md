SteamworksParser
=======

This is a simple parser for the [Steamworks](https://partner.steamgames.com/) header files that I hacked together. You might be wondering why not just use something like libclang to parse the C++. The primary reason was that I wanted to retain comments and formating information.

SteamworksParser is used to generate the [CSteamworks](https://github.com/rlabrecque/CSteamworks) and [Steamworks.NET](https://github.com/rlabrecque/Steamworks.NET) bindings.

Usage Example:

Pull this package into your project folder.

	import sys
	from SteamworksParser import steamworksparser
	
	def main():
		if len(sys.argv) != 2:
			print('Usage: test.py <path/to/steamworks_sdk_135/sdk/public/steam/>')
			return
	
		steamworksparser.Settings.warn_utf8bom = True
		steamworksparser.Settings.warn_includeguardname = True
		steamworksparser.Settings.warn_spacing = True
		parser = steamworksparser.parse(sys.argv[1])
	
		with open('test.json', 'w') as out:
			out.write('{\n')
	
			out.write('    "typedefs":[\n')
			for typedef in parser.typedefs:
				out.write('        {\n')
				out.write('            "typedef":"' + typedef.name + '",\n')
				out.write('            "type":"' + typedef.type + '"\n')
				out.write('        },\n')
	
	
	if __name__ == '__main__':
		main()
