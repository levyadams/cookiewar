<script context="module">

export const locations = [
    {
        name:'brownstown',
        cookieWeight: .5,
        priceSpread:8,
        localPrices: [
            {name:'semonas',price:0},
            {name:'mintz',price:0},
            {name:'shmores',price:0},
            {name:'chipz',price:0},
            {name:'wagalongs',price:0},
            {name:'patties',price:0}
        ]
    },
    {
        name:'Le Pew',
        cookieWeight: 1.5,
        priceSpread:8,
        localPrices: [
            {name:'semonas',price:0},
            {name:'mintz',price:0},
            {name:'shmores',price:0},
            {name:'chipz',price:0},
            {name:'wagalongs',price:0},
            {name:'patties',price:0}
        ]
    }
];

export const cookies = [
    {
        name:'semonas',
        icon:'icon-spinner5',
        minPrice:10,
        maxPrice:700
    },
    {
        name:'mintz',
        icon:'icon-spinner5',

        minPrice:1,
        maxPrice:50

    },
    {
        name:'shmores',
        icon:'icon-spinner5',

        minPrice:5,
        maxPrice:100

    },
    {
        name:'chipz',
        icon:'icon-spinner5',

        minPrice:1,
        maxPrice:20

    },
    {
        name:'wagalongs',
        icon:'icon-spinner5',
        minPrice:5,
        maxPrice:60
    },
    {
        name:'patties',
        icon:'icon-spinner5',
        minPrice:10,
        maxPrice:200
    }

];

</script>