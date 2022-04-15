## Condition inside project    

    {
        $project: {
        vehicleImage: 1,
        name: 1,
        isDeleted: 1,
        brandId: 1,
        model: 1,
        status: 1,
        createdAt: 1,
        updatedAt: 1,
        location: 1,
        kmDriven: 1,
        bodyType: 1,
        damageDetails: 1,
        color: 1,
        price: 1,
        liveAuctionStartDateAndTime: 1,
        liveAuctionEndDateAndTime: 1,
        plateNumber: 1,
        year: 1,
        fuelType: 1,
        description: 1,
        transmissionType: 1,
        vehicleList: 1,
        vehicleGroup: 1,
        city: 1,
        isFavourite: {
            $cond: {
            if: {
                $eq: [
                {
                    $size: '$isFavourite'
                },
                1
                ]
            },
            then: true,
            else: false
            }
        }
        },
    },
