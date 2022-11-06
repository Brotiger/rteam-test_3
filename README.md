![Last commit](https://img.shields.io/github/last-commit/brotiger/rteam_test_3)

# RTeam
## Тестовое задание №3
Задание - [https://drive.google.com/file/d/16Z0k5CoZqq4ufChQIVMBnx2Fgd8zeHHg/view?usp=sharing](https://drive.google.com/file/d/16Z0k5CoZqq4ufChQIVMBnx2Fgd8zeHHg/view?usp=sharing) 

### Пункт №1

    db.Documents.updateMany(
	    {
		    type: "News",
		    media:
		    {
			    $elemMatch: {
				    provider: "youtube"
			    }
		    },
		    status: 
		    { 
			    $ne: "deleted"
		    }
	    },
	    {
		    $set: {
			    "media.$.published": false	
		    }
	    }
    )

### Пункт №2

    db.Documents.aggregate(
        [
            {
                $match: {
                    type: { 
                            $ne: "News"
                        },
                    },
            },
            {$unwind: '$media'},
            {
                $match: {
                    $and: [
                        {
                            "media.provider" : "youtube"
                        },
                        {
                            "media.published" : true
                        }
                    ]
                }
            },
            {
                $count: "media_count"
            }
        ]
    )