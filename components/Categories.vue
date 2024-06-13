<script lang="jsx" setup>
const lang = useState("lang")

const { category, products, maxLevel, minLevel, showAllImgs } = defineProps(["category", "products", "maxLevel", "minLevel", "showAllImgs"])

const CategoryWrapper = defineComponent(() => {
    let ret = [];

    if (maxLevel !== undefined && minLevel !== undefined) {
        if (category.level >= minLevel && category.level <= maxLevel) {
            if (category.level > 0)
                ret.push(<CategoryBtn />)
        }
    } else {
        if (category.level > 0)
            ret.push(<CategoryBtn />)
    }

    if (category.hasOwnProperty('categories')) {
        ret.push(<CategorySubLevels />)
    }

    return () => <div class={'category-wrapper'}>
        {ret}
    </div>
})

const CategorySubLevels = defineComponent(() => {
    let ret = []

    if (category.hasOwnProperty('categories')) {
        for (let c of category.categories) {
            ret.push(<Categories category={c} products={products} maxLevel={maxLevel} minLevel={minLevel} showAllImgs={showAllImgs} />)
        }

        return () => <div name={category.id} class={'level-' + category.level}  >
            {ret}
        </div>
    }
})

const CategoryBtn = defineComponent(() => {

    return () => <div class={"categoryBtn open"} id={category.id} >
        <NuxtLink to={'/categories/' + category.id}>
            <CategoryImg />
            {category.name[lang.value]}
        </NuxtLink>
    </div>
})

const CategoryImg = defineComponent(() => {
    let img;
    if (category.hasOwnProperty('image')) {
        img = <div class="category_img" style={'background-image:url(' + category.image + ')'}></div>
    } else {
        img = []

        if (products) {
            if (showAllImgs) {
                let imgs = []
                for (let p of products) {
                    if (p.categories.includes(category.id) && p.images && p.images.length > 0) {
                        for (const i of p.images) {
                            imgs.push(<div class="category_img" style={'background-image:url(' + i + ')'}></div>)
                        }
                    }
                }
                img.push(<div class="category_img_wrapper">{imgs}</div>)
            } else {
                for (let p of products) {
                    if (p.categories.includes(category.id) && p.images && p.images.length > 0) {
                        img.push(<div class="category_img" style={'background-image:url(' + p.images[0] + ')'}></div>)
                        break
                    }
                }
            }
        }
    }

    if (!img) {
        return
    }

    return () => img
})

</script>

<template>
    <div v-if="category"
        :class="'level-grp ' + (category.hasOwnProperty('categories') ? 'hasSubLevels' : 'noSubLevels')">
        <CategoryWrapper v-if="category.level > 0" />
        <CategoryWrapper v-else />
    </div>
</template>



<style>

#app > .level-grp {
    margin-left: 42px;
    margin-top: 10px;
}

.categoryBtn a.router-link-exact-active {
    text-decoration: underline;
    font-weight: bold;
}

.categoryBtn {
    margin: 0;
    position: relative;
}

.categoryBtn a {
    color: var(--text-color);
    text-decoration: none;
}

.categoryBtn a:hover {
    text-decoration: underline;
    font-weight: bold;
}


.level-0 {
    font-size: 2.5rem;

    display: grid;
    grid-template-columns: repeat(2, 1fr);
}

.level-1 {
    font-size: 2rem;

    display: grid;
    grid-template-columns: repeat(2, 1fr);
}

.level-2 {
    font-size: 1rem;
    font-weight: bold;
    display: inline;
}

.level-3 {
    font-weight: normal;
}


#front-categories .category_img {
    position: relative;

    min-width: 10px;
    min-height: 10px;
    width: 100%;
    height: 75vh;

    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
}
</style>