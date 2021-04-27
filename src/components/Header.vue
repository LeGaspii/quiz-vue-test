<template>
    <div>
        <b-nav tabs>
            <b-nav-item disabled><b>Fancy Quiz Of The Deadly Death</b></b-nav-item>
            <b-nav-item disabled>Counter: {{ numCorrect }}/ {{ numTotal}}</b-nav-item>
        </b-nav>
    </div>
</template>

<script>
export default {
    props: [
        'numCorrect',
        'numTotal'
    ]
}
</script>