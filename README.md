Thanks a lot for taking the time to work on this challenge. 

We want you to have a glimpse on a very simplified version of the tasks we are working on. 

Personalisation matters for us. For this purpose we collected `product_view` and `purchase` events. As an applied scientist in the Recommendation & Personalisation team, we kindly ask you to analyse events and try to predict for every user `size` and `price` preferences. Those preferences can be a range or directly a value. You can chose the response data structure.

(Optionally) If you want you can also add how certain is your prediction per user and property.

Please include the project with all the source code as a zip/tar.gz file.

You are free to use any library or programming language. It can be notebook file, just one file script or even a dockerized project, completely your decision. We would like to run the project in our local machines easily. 

`events.log` file is in JSONL format. Every row has an event serialized as json with the properties:
{
    "user_id": used id of the event,
    "event": name of the event, (`product_view` or `purchase`)
    "price": price of the product,
    "size": size of the product
}

We hope you will have fun while working on the project.

