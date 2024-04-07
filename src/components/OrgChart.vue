<template>
    <div  id="tree" ref="tree"></div>
</template>

<script>
import OrgChart from '@balkangraph/orgchart.js';

export default {
    name: 'TreeComponent',
    data() {
        return {
            nodes: [
            { id: "1", name: "Management Team" , department : "aaaa" , numberOfEmployees : 5 },
            { id: "2", pid: "1", name: "IT Team" , department : "bbb" , numberOfEmployees : 3},
            // { id: "3", pid: "2", name: "Marketing Team" , department : "cccc" , numberOfEmployees : 6},
            // { id: "4", pid: "2", name: "Marketing Team" , department : "cccc" , numberOfEmployees : 7},
            // { id: "5", pid: "3", name: "Marketing Team" , department : "cccc" , numberOfEmployees : 2},
            // { id: "6", pid: "3", name: "Marketing Team" , department : "cccc" , numberOfEmployees : 4},
            // { id: "7", pid: "4", name: "Marketing Team" , department : "cccc" , numberOfEmployees : 6},
            ]
        }
    },
    mounted() {
        // Define OrgChart.templates
        OrgChart.templates.ana = Object.assign({}, OrgChart.templates.ana, {
            text_0: '<text style="font-size: 20px;" fill="#ffffff" x="40" y="30" text-anchor="start">{val}</text>',
            text_1: '<text style="font-size: 20px;" fill="#ffffff" x="220" y="30" text-anchor="middle">{val}</text>',
            text_2: '<text style="font-size: 20px;" fill="#ffffff" x="40" y="100" text-anchor="start">{val}</text>',
            text_3: '<text style="font-size: 20px;" fill="#ffffff" x="220" y="100" text-anchor="start">{val}</text>'
        });

        const domEl = this.$refs.tree;
        this.chart = new OrgChart(domEl, {
            nodes: this.nodes,
            nodeBinding: {
                text_0: "department",
                text_1:"numberOfEmployees",
                text_2:"name",
                text_3:"numberOfEmployees",
            },
            template: "ana",
            menu: {
            pdf: { text: "Export PDF" },
            png: { text: "Export PNG" },
            svg: { text: "Export SVG" },
            csv: { text: "Export CSV" },
            json: { text: "Export JSON" }
        },
        });
        console.log(this.chart.onExpandCollpaseButtonClick(() => {
            //return false; to cancel the operation
            this.nodes.push({ id: "2", pid: "1", name: "IT Team" , department : "bbb" , numberOfEmployees : 3})
        console.log("aaa");
        }));
    }
};
</script>