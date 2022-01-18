# Hosting Static Website using AWS S3
[Vist My Website - Burger Exchange](http://static-webpagebucket.s3-website.us-east-2.amazonaws.com)
 
 Follwing are Steps to Host a Website on AWS S3
 
 1. Create an S3 Bucket , disbale "Block all Public Access" while creating the S3 Bucket
 ![alt text](https://bucketforowork.s3.us-east-2.amazonaws.com/staticwebpage/public-access.PNG?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjELj%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCmFwLXNvdXRoLTEiSDBGAiEA0TPf1vvOPl%2FwVOYr5vwD%2Fr2EOzaMJf3Cxf5bbXN4CZoCIQCLEqK5TMGFEDXmuvePiss%2FhojYOHuwavW1uMexu5y6RyrxAgjR%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDY3NTkxNDgzOTM2OSIM0fR2NlWDtWX4yKGfKsUCz9pm3DtAYzV6PVcxEMdYVQYH7pxbnY8gVV7gaxyPSQJVOhDZkRea492%2FDJEfNX6ysqFBlPvVuSZmqeJe7w2RMyXA7Tr%2FVJCwky%2FYu0xXW7k8WacPTObA0Uo%2F0itvWIxsa6DgoxGBpl7puOx1rsHuyNmf9%2FxJ26G6QW118UHSG%2FM7YZGMGXN9RnzDOVeQPtYbVetp2JfhdNXdlaYCJgEhHenidpgjKeh2FxFTj68%2BAEo3GYEqO2jAj%2F1Zlq8xElDGgnZsDexc3aFVzpqEGE8V1eBch6fiOwLsYLvlB4YfxugKz4hiRBjTVfFkOu3FiHk0sSsDaG%2BSuVjceQsM5ADn6luB4GTmy802zRQe8mofmNUpvQ%2B5QhyDP3GKqd1OUhfyEYN99VH6uIgvKGndgyejKTd1Nu49d2Cjdp3dae5nUcg2gVPhxTDS3pmPBjqyAscGqvZdb5BDmvePtqzEQKTWMzBc1uVKYmGCIpQhqltzGif5YryFfWXkEz2kdApTXuZk70dIVT9PcAgJqafC4UxBSScuD7mx4P5mcb0c%2FBOFKKgeWf%2BrdK8P6H4cAUkLaVP3vsJGlWmuXHb2%2B4trbuTJNRZZt%2B6BJPPznaXwq8PgFdavOTwjsKHrdprJ13RsL5usgKaaJCF2BOzMG1E%2BDsDZ9ghmQVH7orxhMgGkGOt%2F4NLexFvYxtyVS6%2BnHQF2Vz9rXbyxCdLOeSkRLUATKpIQ79YfSQkVC3zUhJwqvPvjd71RWatnzcVniXekyazeuKKBm%2FTD82gvIHBed5DGzxptC22o83lfU%2F0wKQ00hciHgHGtPxW91mQJus5yRyuou1COREFCAeiKUJ7IlwQdnoU2Dw%3D%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20220118T075021Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAZ2X5J6VEVR3BW2MH%2F20220118%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Signature=bbc308172bd7cad5dfeb1839af561b6d7625b1b654b808418eda7a3ba565de15)
 
 2.Upload your files in the bucket
 ![alt text](https://bucketforowork.s3.us-east-2.amazonaws.com/staticwebpage/uploadefiles.PNG?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjELj%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCmFwLXNvdXRoLTEiSDBGAiEA0TPf1vvOPl%2FwVOYr5vwD%2Fr2EOzaMJf3Cxf5bbXN4CZoCIQCLEqK5TMGFEDXmuvePiss%2FhojYOHuwavW1uMexu5y6RyrxAgjR%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDY3NTkxNDgzOTM2OSIM0fR2NlWDtWX4yKGfKsUCz9pm3DtAYzV6PVcxEMdYVQYH7pxbnY8gVV7gaxyPSQJVOhDZkRea492%2FDJEfNX6ysqFBlPvVuSZmqeJe7w2RMyXA7Tr%2FVJCwky%2FYu0xXW7k8WacPTObA0Uo%2F0itvWIxsa6DgoxGBpl7puOx1rsHuyNmf9%2FxJ26G6QW118UHSG%2FM7YZGMGXN9RnzDOVeQPtYbVetp2JfhdNXdlaYCJgEhHenidpgjKeh2FxFTj68%2BAEo3GYEqO2jAj%2F1Zlq8xElDGgnZsDexc3aFVzpqEGE8V1eBch6fiOwLsYLvlB4YfxugKz4hiRBjTVfFkOu3FiHk0sSsDaG%2BSuVjceQsM5ADn6luB4GTmy802zRQe8mofmNUpvQ%2B5QhyDP3GKqd1OUhfyEYN99VH6uIgvKGndgyejKTd1Nu49d2Cjdp3dae5nUcg2gVPhxTDS3pmPBjqyAscGqvZdb5BDmvePtqzEQKTWMzBc1uVKYmGCIpQhqltzGif5YryFfWXkEz2kdApTXuZk70dIVT9PcAgJqafC4UxBSScuD7mx4P5mcb0c%2FBOFKKgeWf%2BrdK8P6H4cAUkLaVP3vsJGlWmuXHb2%2B4trbuTJNRZZt%2B6BJPPznaXwq8PgFdavOTwjsKHrdprJ13RsL5usgKaaJCF2BOzMG1E%2BDsDZ9ghmQVH7orxhMgGkGOt%2F4NLexFvYxtyVS6%2BnHQF2Vz9rXbyxCdLOeSkRLUATKpIQ79YfSQkVC3zUhJwqvPvjd71RWatnzcVniXekyazeuKKBm%2FTD82gvIHBed5DGzxptC22o83lfU%2F0wKQ00hciHgHGtPxW91mQJus5yRyuou1COREFCAeiKUJ7IlwQdnoU2Dw%3D%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20220118T075609Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAZ2X5J6VEVR3BW2MH%2F20220118%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Signature=b1d5e2c7e3b875617b2efa6a04c0a53a8123b50de90d6b3bb7ce3553f54e7c49)
 
 3.Select your Bucket and goto Bucket Propoerties
 
 4.Edit "Static website hosting"
 
 5.Enable "Static Website Hosting"
 
 6.Specify Hosting Type , since we want to host static website in current bucket we will select Hosting Type-"Host a static website" 
 
 7.Specify the "index document" i.e. the home page of your website
 
 8.Specify the "error document" , it is optional and Save Changes
 
 ![alt text](https://bucketforowork.s3.us-east-2.amazonaws.com/staticwebpage/enabling.PNG?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjELj%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCmFwLXNvdXRoLTEiSDBGAiEA0TPf1vvOPl%2FwVOYr5vwD%2Fr2EOzaMJf3Cxf5bbXN4CZoCIQCLEqK5TMGFEDXmuvePiss%2FhojYOHuwavW1uMexu5y6RyrxAgjR%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDY3NTkxNDgzOTM2OSIM0fR2NlWDtWX4yKGfKsUCz9pm3DtAYzV6PVcxEMdYVQYH7pxbnY8gVV7gaxyPSQJVOhDZkRea492%2FDJEfNX6ysqFBlPvVuSZmqeJe7w2RMyXA7Tr%2FVJCwky%2FYu0xXW7k8WacPTObA0Uo%2F0itvWIxsa6DgoxGBpl7puOx1rsHuyNmf9%2FxJ26G6QW118UHSG%2FM7YZGMGXN9RnzDOVeQPtYbVetp2JfhdNXdlaYCJgEhHenidpgjKeh2FxFTj68%2BAEo3GYEqO2jAj%2F1Zlq8xElDGgnZsDexc3aFVzpqEGE8V1eBch6fiOwLsYLvlB4YfxugKz4hiRBjTVfFkOu3FiHk0sSsDaG%2BSuVjceQsM5ADn6luB4GTmy802zRQe8mofmNUpvQ%2B5QhyDP3GKqd1OUhfyEYN99VH6uIgvKGndgyejKTd1Nu49d2Cjdp3dae5nUcg2gVPhxTDS3pmPBjqyAscGqvZdb5BDmvePtqzEQKTWMzBc1uVKYmGCIpQhqltzGif5YryFfWXkEz2kdApTXuZk70dIVT9PcAgJqafC4UxBSScuD7mx4P5mcb0c%2FBOFKKgeWf%2BrdK8P6H4cAUkLaVP3vsJGlWmuXHb2%2B4trbuTJNRZZt%2B6BJPPznaXwq8PgFdavOTwjsKHrdprJ13RsL5usgKaaJCF2BOzMG1E%2BDsDZ9ghmQVH7orxhMgGkGOt%2F4NLexFvYxtyVS6%2BnHQF2Vz9rXbyxCdLOeSkRLUATKpIQ79YfSQkVC3zUhJwqvPvjd71RWatnzcVniXekyazeuKKBm%2FTD82gvIHBed5DGzxptC22o83lfU%2F0wKQ00hciHgHGtPxW91mQJus5yRyuou1COREFCAeiKUJ7IlwQdnoU2Dw%3D%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20220118T080732Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAZ2X5J6VEVR3BW2MH%2F20220118%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Signature=a2074e1befcc11e1056c6df40efaaeeb60924983160244e427442a3303b9dbd6)
 
 9.Select your Bucket and goto "Permissions"
 
      1. Disable Block Public Aceess (already done in Step 1)
      2.Edit the Bucket Policy to enable Public Read Access to your Website , update the Bucket Policy as below,
        replace Bucket-Name with your Bucket's Name
         
                                   {
                              "Version": "2012-10-17",
                              "Statement": [
                                  {
                                      "Sid": "PublicReadGetObject",
                                      "Effect": "Allow",
                                      "Principal": "*",
                                      "Action": [
                                          "s3:GetObject"
                                      ],
                                      "Resource": [
                                          "arn:aws:s3:::Bucket-Name/*"
                                      ]
                                  }
                              ]
                          }
      
      3.Save Changes
      
      
10. Website on S3 Bucket is now Publicly accessible as shown in below Snip
![alt text](https://bucketforowork.s3.us-east-2.amazonaws.com/staticwebpage/final.PNG?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjELj%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCmFwLXNvdXRoLTEiSDBGAiEA0TPf1vvOPl%2FwVOYr5vwD%2Fr2EOzaMJf3Cxf5bbXN4CZoCIQCLEqK5TMGFEDXmuvePiss%2FhojYOHuwavW1uMexu5y6RyrxAgjR%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDY3NTkxNDgzOTM2OSIM0fR2NlWDtWX4yKGfKsUCz9pm3DtAYzV6PVcxEMdYVQYH7pxbnY8gVV7gaxyPSQJVOhDZkRea492%2FDJEfNX6ysqFBlPvVuSZmqeJe7w2RMyXA7Tr%2FVJCwky%2FYu0xXW7k8WacPTObA0Uo%2F0itvWIxsa6DgoxGBpl7puOx1rsHuyNmf9%2FxJ26G6QW118UHSG%2FM7YZGMGXN9RnzDOVeQPtYbVetp2JfhdNXdlaYCJgEhHenidpgjKeh2FxFTj68%2BAEo3GYEqO2jAj%2F1Zlq8xElDGgnZsDexc3aFVzpqEGE8V1eBch6fiOwLsYLvlB4YfxugKz4hiRBjTVfFkOu3FiHk0sSsDaG%2BSuVjceQsM5ADn6luB4GTmy802zRQe8mofmNUpvQ%2B5QhyDP3GKqd1OUhfyEYN99VH6uIgvKGndgyejKTd1Nu49d2Cjdp3dae5nUcg2gVPhxTDS3pmPBjqyAscGqvZdb5BDmvePtqzEQKTWMzBc1uVKYmGCIpQhqltzGif5YryFfWXkEz2kdApTXuZk70dIVT9PcAgJqafC4UxBSScuD7mx4P5mcb0c%2FBOFKKgeWf%2BrdK8P6H4cAUkLaVP3vsJGlWmuXHb2%2B4trbuTJNRZZt%2B6BJPPznaXwq8PgFdavOTwjsKHrdprJ13RsL5usgKaaJCF2BOzMG1E%2BDsDZ9ghmQVH7orxhMgGkGOt%2F4NLexFvYxtyVS6%2BnHQF2Vz9rXbyxCdLOeSkRLUATKpIQ79YfSQkVC3zUhJwqvPvjd71RWatnzcVniXekyazeuKKBm%2FTD82gvIHBed5DGzxptC22o83lfU%2F0wKQ00hciHgHGtPxW91mQJus5yRyuou1COREFCAeiKUJ7IlwQdnoU2Dw%3D%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20220118T082151Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAZ2X5J6VEVR3BW2MH%2F20220118%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Signature=9b48b7f0d7843e00ccdecdbeba304d14982f0fb25e9e03b5b73bfaa8232742b2)


11. Goto the "Bucket Website Endpoint" and select Bucket Endpoint to access the Website on web.
[My Website - Burger Exchange](http://static-webpagebucket.s3-website.us-east-2.amazonaws.com)

![alt text](https://bucketforowork.s3.us-east-2.amazonaws.com/staticwebpage/endpoint.PNG?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjELj%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCmFwLXNvdXRoLTEiSDBGAiEA0TPf1vvOPl%2FwVOYr5vwD%2Fr2EOzaMJf3Cxf5bbXN4CZoCIQCLEqK5TMGFEDXmuvePiss%2FhojYOHuwavW1uMexu5y6RyrxAgjR%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDY3NTkxNDgzOTM2OSIM0fR2NlWDtWX4yKGfKsUCz9pm3DtAYzV6PVcxEMdYVQYH7pxbnY8gVV7gaxyPSQJVOhDZkRea492%2FDJEfNX6ysqFBlPvVuSZmqeJe7w2RMyXA7Tr%2FVJCwky%2FYu0xXW7k8WacPTObA0Uo%2F0itvWIxsa6DgoxGBpl7puOx1rsHuyNmf9%2FxJ26G6QW118UHSG%2FM7YZGMGXN9RnzDOVeQPtYbVetp2JfhdNXdlaYCJgEhHenidpgjKeh2FxFTj68%2BAEo3GYEqO2jAj%2F1Zlq8xElDGgnZsDexc3aFVzpqEGE8V1eBch6fiOwLsYLvlB4YfxugKz4hiRBjTVfFkOu3FiHk0sSsDaG%2BSuVjceQsM5ADn6luB4GTmy802zRQe8mofmNUpvQ%2B5QhyDP3GKqd1OUhfyEYN99VH6uIgvKGndgyejKTd1Nu49d2Cjdp3dae5nUcg2gVPhxTDS3pmPBjqyAscGqvZdb5BDmvePtqzEQKTWMzBc1uVKYmGCIpQhqltzGif5YryFfWXkEz2kdApTXuZk70dIVT9PcAgJqafC4UxBSScuD7mx4P5mcb0c%2FBOFKKgeWf%2BrdK8P6H4cAUkLaVP3vsJGlWmuXHb2%2B4trbuTJNRZZt%2B6BJPPznaXwq8PgFdavOTwjsKHrdprJ13RsL5usgKaaJCF2BOzMG1E%2BDsDZ9ghmQVH7orxhMgGkGOt%2F4NLexFvYxtyVS6%2BnHQF2Vz9rXbyxCdLOeSkRLUATKpIQ79YfSQkVC3zUhJwqvPvjd71RWatnzcVniXekyazeuKKBm%2FTD82gvIHBed5DGzxptC22o83lfU%2F0wKQ00hciHgHGtPxW91mQJus5yRyuou1COREFCAeiKUJ7IlwQdnoU2Dw%3D%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20220118T082233Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAZ2X5J6VEVR3BW2MH%2F20220118%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Signature=87e6138c677ed2e22f922f3073df0def0050f9245fee9076c214cc23b018eb1f)

