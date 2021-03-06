README for Imagoxy 0.54
==============================

Imagoxy ("image proxy") is a tiny PHP toolkit. It downloads pictures from remote server to local server and relocate corresponding http requests to the local one. It is used to access pictures when the remote server is banned or slow from the network of clients (e.g. Download pictures from Picasa on an unbanned US server and tranfer them to China's viewers where Picasa is banned sometimes).

Licensed under a BSD license.

Install:

1. Modify Imagoxy 'getimg.php' file:
	* Set '$work_dir' to the location you wish Imagoxy works at.
	* Set '$cache_dir' to the location you wish files downloaded to. (default is OK in most cases)
	* Set '$error_file' as the file relocated to when access control denied. (default is OK in most cases)
	* Set '$reffer_list' as the legal HTTP_REFERER prefix list.
	* Set '$check_reffer_before_download' as whether to check HTTP_REFERER before downloading new picutre.
	* Set '$check_reffer_before_show' as whether to check HTTP_REFERER before showing downloaded picutre.
	* Set '$legal_pattern' as the legal file URL patterns. (default is for Picasa and Flickr; you can add more)
2. Update the 'imagoxy' directory to your '$work_dir' and make the '$cache_dir' writable.
3. Configure and deploy Imagoxy front-ends such as Imagoxy-WP.

Usage:

1. [ http://www.example.com/imagoxy/getimg.php?s={original URL} ] In this format (we called 'Imagoxy URL'), the http request will be relocated to a file on local server which is downloaded from the original URL. You can embed the Imagoxy URL into your <img src="..."> label. 'http://' in original URL is omissible and the other protocols are not allowed. Notice: as a parameter, original URL should be url-encoded again even if it has been url-encoded. e.g. 'Pic%20A.jpg' -> 'Pic%2520A.jpg'.
2. [ http://www.example.com/imagoxy/getimg.php?u={encoded URL} ] Also does downloading and relocation. However, you should base64-encode, reverse and then url-encode the original URL. In PHP, these are done by 'urlencode(strrev(base64_encode($original_url)))'. This encoding method can pass the URL filter in certain regions.

Test:

You can write a html page with an Imagoxy URL in <img src="..."> label. Open it locally, you should see the '$error_file'; after uploading it to the server with the URL prefix in '$reffer_list', you will see the relocated picture correctly.

Example:

I have a picture named "火车   测试-+=_  [.a.] 图片  pic.JPG" (encoded in zh_CN.utf_8) on Picasa:

	* Normal Picasa URL:
	http://lh5.ggpht.com/_ZQ_-T1yEBQY/SmQSOX5_xFI/AAAAAAAABPY/h8Tw6PWuZP8/%E7%81%AB%E8%BD%A6%20%20%20%E6%B5%8B%E8%AF%95-%2B%3D_%20%20%5B.a.%5D%20%E5%9B%BE%E7%89%87%20%20pic.JPG

	* Normal Picasa URL with query string "imgmax":
	http://lh5.ggpht.com/_ZQ_-T1yEBQY/SmQSOX5_xFI/AAAAAAAABPY/h8Tw6PWuZP8/%E7%81%AB%E8%BD%A6%20%20%20%E6%B5%8B%E8%AF%95-%2B%3D_%20%20%5B.a.%5D%20%E5%9B%BE%E7%89%87%20%20pic.JPG?imgmax=200

	* Imagoxy URL (parameter 's') [Noted that the URL should be url-encoded again as a parameter! '%' -> '%25']:
	http://www.example.com/imagoxy/getimg.php?s=http://lh5.ggpht.com/_ZQ_-T1yEBQY/SmQSOX5_xFI/AAAAAAAABPY/h8Tw6PWuZP8/%25E7%2581%25AB%25E8%25BD%25A6%2520%2520%2520%25E6%25B5%258B%25E8%25AF%2595-%252B%253D_%2520%2520%255B.a.%255D%2520%25E5%259B%25BE%25E7%2589%2587%2520%2520pic.JPG

	* Imagoxy URL (parameter 's')  with query string "imgmax":
	http://www.example.com/imagoxy/getimg.php?s=http://lh5.ggpht.com/_ZQ_-T1yEBQY/SmQSOX5_xFI/AAAAAAAABPY/h8Tw6PWuZP8/%25E7%2581%25AB%25E8%25BD%25A6%2520%2520%2520%25E6%25B5%258B%25E8%25AF%2595-%252B%253D_%2520%2520%255B.a.%255D%2520%25E5%259B%25BE%25E7%2589%2587%2520%2520pic.JPG?imgmax=200

	* Imagoxy URL (parameter 'u') [Parameter made by Imagoxy-WP]:
	http://www.example.com/imagoxy/getimg.php?u=%3D%3DwRQpkLjlGcwITJwITJ3gTJ5gTJ3UUJFJUJClTJ1UUJwITJEVTJuEmLCVTJwITJwITJfR0MlIkMl0SN5UiRBVCOFViQ4USNCViNFVCMyUCMyUCMyUiNBVCRCVCOFViQBVSM4UyNFVyL4AlW1dFU2cHV4g2LZBlQBFUQBFUQBF0LJZEefVDWPNVUtN1LZFlQFlXMU1yXRp1Xv02bj5CdoB3Zn5SNox2LvoDc0RHa

	* Imagoxy URL (parameter 'u') with query string "imgmax":
	http://www.example.com/imagoxy/getimg.php?u=wAjM9gXYtdWbp9zRQpkLjlGcwITJwITJ3gTJ5gTJ3UUJFJUJClTJ1UUJwITJEVTJuEmLCVTJwITJwITJfR0MlIkMl0SN5UiRBVCOFViQ4USNCViNFVCMyUCMyUCMyUiNBVCRCVCOFViQBVSM4UyNFVyL4AlW1dFU2cHV4g2LZBlQBFUQBFUQBF0LJZEefVDWPNVUtN1LZFlQFlXMU1yXRp1Xv02bj5CdoB3Zn5SNox2LvoDc0RHa

Enjoy it!

Jian Lin <lj [at] linjian [dot] org>
2011-03-02
