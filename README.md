# prometheus
## enter google cloud shell and do this commands:
### commands:
1. kind create cluster --name=snir
2. helm repo add prometheus-community https://prometheuscommunity.github.io/helm-charts
3. helm repo update
4. kubectl create namespace monitoring
5. helm install prometheus prometheus-community/kube-prometheus-stack -n monitoring
6. wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz 
7. tar -zxvf ngrok-v3-stable-linux-amd64.tgz 
8. ./ngrok config add-authtoken 2QCcclEE80tINnI1Gx8QMyKLFbr_4hscbjiAdumc5BjHBiNwN
9. kubectl port-forward service/prometheus-kube-prometheus-prometheus -n monitoring 9090:9090 --address='0.0.0.0' &
10. kubectl port-forward service/prometheus-grafana -n monitoring 8080:80 --address='0.0.0.0' &
11. ./ngrok http 0.0.0.0:9090

i take the Kubernetes/Compute Resources/Cluster Dashboard and edit it and delete the panels idint need and this is the json for the first dashborod:
{
  "annotations": {
    "list": [
      {
        "builtIn": 1,
        "datasource": {
          "type": "grafana",
          "uid": "-- Grafana --"
        },
        "enable": true,
        "hide": true,
        "iconColor": "rgba(0, 211, 255, 1)",
        "name": "Annotations & Alerts",
        "type": "dashboard"
      }
    ]
  },
  "editable": true,
  "fiscalYearStartMonth": 0,
  "graphTooltip": 0,
  "links": [],
  "liveNow": false,
  "panels": [
    {
      "collapsed": false,
      "datasource": {
        "type": "prometheus",
        "uid": "prometheus"
      },
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 0
      },
      "id": 23,
      "panels": [],
      "targets": [
        {
          "datasource": {
            "type": "prometheus",
            "uid": "prometheus"
          },
          "refId": "A"
        }
      ],
      "title": "Headlines",
      "type": "row"
    },
    {
      "datasource": {
        "uid": "$datasource"
      },
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          },
          "unit": "percentunit"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 3,
        "w": 4,
        "x": 0,
        "y": 1
      },
      "id": 1,
      "interval": "1m",
      "links": [],
      "options": {
        "colorMode": "none",
        "graphMode": "none",
        "justifyMode": "auto",
        "orientation": "horizontal",
        "reduceOptions": {
          "calcs": [
            "mean"
          ],
          "fields": "",
          "values": false
        },
        "textMode": "auto"
      },
      "pluginVersion": "9.5.5",
      "targets": [
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "cluster:node_cpu:ratio_rate5m{cluster=\"$cluster\"}",
          "format": "time_series",
          "instant": true,
          "intervalFactor": 2,
          "refId": "A"
        }
      ],
      "title": "CPU Utilisation",
      "type": "stat"
    },
    {
      "datasource": {
        "uid": "$datasource"
      },
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          },
          "unit": "percentunit"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 3,
        "w": 4,
        "x": 4,
        "y": 1
      },
      "id": 2,
      "interval": "1m",
      "links": [],
      "options": {
        "colorMode": "none",
        "graphMode": "none",
        "justifyMode": "auto",
        "orientation": "horizontal",
        "reduceOptions": {
          "calcs": [
            "mean"
          ],
          "fields": "",
          "values": false
        },
        "textMode": "auto"
      },
      "pluginVersion": "9.5.5",
      "targets": [
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(namespace_cpu:kube_pod_container_resource_requests:sum{cluster=\"$cluster\"}) / sum(kube_node_status_allocatable{job=\"kube-state-metrics\",resource=\"cpu\",cluster=\"$cluster\"})",
          "format": "time_series",
          "instant": true,
          "intervalFactor": 2,
          "refId": "A"
        }
      ],
      "title": "CPU Requests Commitment",
      "type": "stat"
    },
    {
      "datasource": {
        "uid": "$datasource"
      },
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          },
          "unit": "percentunit"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 3,
        "w": 4,
        "x": 8,
        "y": 1
      },
      "id": 3,
      "interval": "1m",
      "links": [],
      "options": {
        "colorMode": "none",
        "graphMode": "none",
        "justifyMode": "auto",
        "orientation": "horizontal",
        "reduceOptions": {
          "calcs": [
            "mean"
          ],
          "fields": "",
          "values": false
        },
        "textMode": "auto"
      },
      "pluginVersion": "9.5.5",
      "targets": [
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(namespace_cpu:kube_pod_container_resource_limits:sum{cluster=\"$cluster\"}) / sum(kube_node_status_allocatable{job=\"kube-state-metrics\",resource=\"cpu\",cluster=\"$cluster\"})",
          "format": "time_series",
          "instant": true,
          "intervalFactor": 2,
          "refId": "A"
        }
      ],
      "title": "CPU Limits Commitment",
      "type": "stat"
    },
    {
      "datasource": {
        "uid": "$datasource"
      },
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          },
          "unit": "percentunit"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 3,
        "w": 4,
        "x": 12,
        "y": 1
      },
      "id": 4,
      "interval": "1m",
      "links": [],
      "options": {
        "colorMode": "none",
        "graphMode": "none",
        "justifyMode": "auto",
        "orientation": "horizontal",
        "reduceOptions": {
          "calcs": [
            "mean"
          ],
          "fields": "",
          "values": false
        },
        "textMode": "auto"
      },
      "pluginVersion": "9.5.5",
      "targets": [
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "1 - sum(:node_memory_MemAvailable_bytes:sum{cluster=\"$cluster\"}) / sum(node_memory_MemTotal_bytes{job=\"node-exporter\",cluster=\"$cluster\"})",
          "format": "time_series",
          "instant": true,
          "intervalFactor": 2,
          "refId": "A"
        }
      ],
      "title": "Memory Utilisation",
      "type": "stat"
    },
    {
      "datasource": {
        "uid": "$datasource"
      },
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          },
          "unit": "percentunit"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 3,
        "w": 4,
        "x": 16,
        "y": 1
      },
      "id": 5,
      "interval": "1m",
      "links": [],
      "options": {
        "colorMode": "none",
        "graphMode": "none",
        "justifyMode": "auto",
        "orientation": "horizontal",
        "reduceOptions": {
          "calcs": [
            "mean"
          ],
          "fields": "",
          "values": false
        },
        "textMode": "auto"
      },
      "pluginVersion": "9.5.5",
      "targets": [
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(namespace_memory:kube_pod_container_resource_requests:sum{cluster=\"$cluster\"}) / sum(kube_node_status_allocatable{job=\"kube-state-metrics\",resource=\"memory\",cluster=\"$cluster\"})",
          "format": "time_series",
          "instant": true,
          "intervalFactor": 2,
          "refId": "A"
        }
      ],
      "title": "Memory Requests Commitment",
      "type": "stat"
    },
    {
      "datasource": {
        "uid": "$datasource"
      },
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              },
              {
                "color": "red",
                "value": 80
              }
            ]
          },
          "unit": "percentunit"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 3,
        "w": 4,
        "x": 20,
        "y": 1
      },
      "id": 6,
      "interval": "1m",
      "links": [],
      "options": {
        "colorMode": "none",
        "graphMode": "none",
        "justifyMode": "auto",
        "orientation": "horizontal",
        "reduceOptions": {
          "calcs": [
            "mean"
          ],
          "fields": "",
          "values": false
        },
        "textMode": "auto"
      },
      "pluginVersion": "9.5.5",
      "targets": [
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(namespace_memory:kube_pod_container_resource_limits:sum{cluster=\"$cluster\"}) / sum(kube_node_status_allocatable{job=\"kube-state-metrics\",resource=\"memory\",cluster=\"$cluster\"})",
          "format": "time_series",
          "instant": true,
          "intervalFactor": 2,
          "refId": "A"
        }
      ],
      "title": "Memory Limits Commitment",
      "type": "stat"
    },
    {
      "collapsed": false,
      "datasource": {
        "type": "prometheus",
        "uid": "prometheus"
      },
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 4
      },
      "id": 24,
      "panels": [],
      "targets": [
        {
          "datasource": {
            "type": "prometheus",
            "uid": "prometheus"
          },
          "refId": "A"
        }
      ],
      "title": "CPU",
      "type": "row"
    },
    {
      "aliasColors": {},
      "bars": false,
      "dashLength": 10,
      "dashes": false,
      "datasource": {
        "uid": "$datasource"
      },
      "fill": 10,
      "fillGradient": 0,
      "gridPos": {
        "h": 7,
        "w": 24,
        "x": 0,
        "y": 5
      },
      "hiddenSeries": false,
      "id": 7,
      "interval": "1m",
      "legend": {
        "alignAsTable": true,
        "avg": false,
        "current": false,
        "max": false,
        "min": false,
        "rightSide": true,
        "show": true,
        "total": false,
        "values": false
      },
      "lines": true,
      "linewidth": 0,
      "links": [],
      "nullPointMode": "null as zero",
      "options": {
        "alertThreshold": true
      },
      "percentage": false,
      "pluginVersion": "9.5.5",
      "pointradius": 5,
      "points": false,
      "renderer": "flot",
      "seriesOverrides": [],
      "spaceLength": 10,
      "stack": true,
      "steppedLine": false,
      "targets": [
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(node_namespace_pod_container:container_cpu_usage_seconds_total:sum_irate{cluster=\"$cluster\"}) by (namespace)",
          "format": "time_series",
          "intervalFactor": 2,
          "legendFormat": "{{namespace}}",
          "refId": "A",
          "step": 10
        }
      ],
      "thresholds": [],
      "timeRegions": [],
      "title": "CPU Usage",
      "tooltip": {
        "shared": false,
        "sort": 2,
        "value_type": "individual"
      },
      "type": "graph",
      "xaxis": {
        "mode": "time",
        "show": true,
        "values": []
      },
      "yaxes": [
        {
          "format": "short",
          "logBase": 1,
          "min": 0,
          "show": true
        },
        {
          "format": "short",
          "logBase": 1,
          "show": false
        }
      ],
      "yaxis": {
        "align": false
      }
    },
    {
      "collapsed": false,
      "datasource": {
        "type": "prometheus",
        "uid": "prometheus"
      },
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 12
      },
      "id": 25,
      "panels": [],
      "targets": [
        {
          "datasource": {
            "type": "prometheus",
            "uid": "prometheus"
          },
          "refId": "A"
        }
      ],
      "title": "CPU Quota",
      "type": "row"
    },
    {
      "aliasColors": {},
      "bars": false,
      "columns": [],
      "dashLength": 10,
      "dashes": false,
      "datasource": {
        "uid": "$datasource"
      },
      "fill": 1,
      "fontSize": "100%",
      "gridPos": {
        "h": 7,
        "w": 24,
        "x": 0,
        "y": 13
      },
      "id": 8,
      "interval": "1m",
      "legend": {
        "alignAsTable": true,
        "avg": false,
        "current": false,
        "max": false,
        "min": false,
        "rightSide": true,
        "show": true,
        "total": false,
        "values": false
      },
      "lines": true,
      "linewidth": 1,
      "links": [],
      "nullPointMode": "null as zero",
      "percentage": false,
      "pointradius": 5,
      "points": false,
      "renderer": "flot",
      "seriesOverrides": [],
      "showHeader": true,
      "sort": {
        "col": 0,
        "desc": true
      },
      "spaceLength": 10,
      "stack": false,
      "steppedLine": false,
      "styles": [
        {
          "alias": "Time",
          "align": "auto",
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "pattern": "Time",
          "type": "hidden"
        },
        {
          "alias": "Pods",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 0,
          "link": true,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down to pods",
          "linkUrl": "/d/85a562078cdf77779eaa1add43ccec1e/k8s-resources-namespace?var-datasource=$datasource&var-cluster=$cluster&var-namespace=$__cell_1",
          "pattern": "Value #A",
          "thresholds": [],
          "type": "number",
          "unit": "short"
        },
        {
          "alias": "Workloads",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 0,
          "link": true,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down to workloads",
          "linkUrl": "/d/a87fb0d919ec0ea5f6543124e16c42a5/k8s-resources-workloads-namespace?var-datasource=$datasource&var-cluster=$cluster&var-namespace=$__cell_1",
          "pattern": "Value #B",
          "thresholds": [],
          "type": "number",
          "unit": "short"
        },
        {
          "alias": "CPU Usage",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "link": false,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down",
          "linkUrl": "",
          "pattern": "Value #C",
          "thresholds": [],
          "type": "number",
          "unit": "short"
        },
        {
          "alias": "CPU Requests",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "link": false,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down",
          "linkUrl": "",
          "pattern": "Value #D",
          "thresholds": [],
          "type": "number",
          "unit": "short"
        },
        {
          "alias": "CPU Requests %",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "link": false,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down",
          "linkUrl": "",
          "pattern": "Value #E",
          "thresholds": [],
          "type": "number",
          "unit": "percentunit"
        },
        {
          "alias": "CPU Limits",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "link": false,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down",
          "linkUrl": "",
          "pattern": "Value #F",
          "thresholds": [],
          "type": "number",
          "unit": "short"
        },
        {
          "alias": "CPU Limits %",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "link": false,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down",
          "linkUrl": "",
          "pattern": "Value #G",
          "thresholds": [],
          "type": "number",
          "unit": "percentunit"
        },
        {
          "alias": "Namespace",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "link": true,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down to pods",
          "linkUrl": "/d/85a562078cdf77779eaa1add43ccec1e/k8s-resources-namespace?var-datasource=$datasource&var-cluster=$cluster&var-namespace=$__cell",
          "pattern": "namespace",
          "thresholds": [],
          "type": "number",
          "unit": "short"
        },
        {
          "alias": "",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "pattern": "/.*/",
          "thresholds": [],
          "type": "string",
          "unit": "short"
        }
      ],
      "targets": [
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(kube_pod_owner{job=\"kube-state-metrics\", cluster=\"$cluster\"}) by (namespace)",
          "format": "table",
          "instant": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "A",
          "step": 10
        },
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "count(avg(namespace_workload_pod:kube_pod_owner:relabel{cluster=\"$cluster\"}) by (workload, namespace)) by (namespace)",
          "format": "table",
          "instant": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "B",
          "step": 10
        },
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(node_namespace_pod_container:container_cpu_usage_seconds_total:sum_irate{cluster=\"$cluster\"}) by (namespace)",
          "format": "table",
          "instant": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "C",
          "step": 10
        },
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(namespace_cpu:kube_pod_container_resource_requests:sum{cluster=\"$cluster\"}) by (namespace)",
          "format": "table",
          "instant": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "D",
          "step": 10
        },
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(node_namespace_pod_container:container_cpu_usage_seconds_total:sum_irate{cluster=\"$cluster\"}) by (namespace) / sum(namespace_cpu:kube_pod_container_resource_requests:sum{cluster=\"$cluster\"}) by (namespace)",
          "format": "table",
          "instant": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "E",
          "step": 10
        },
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(namespace_cpu:kube_pod_container_resource_limits:sum{cluster=\"$cluster\"}) by (namespace)",
          "format": "table",
          "instant": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "F",
          "step": 10
        },
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(node_namespace_pod_container:container_cpu_usage_seconds_total:sum_irate{cluster=\"$cluster\"}) by (namespace) / sum(namespace_cpu:kube_pod_container_resource_limits:sum{cluster=\"$cluster\"}) by (namespace)",
          "format": "table",
          "instant": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "G",
          "step": 10
        }
      ],
      "thresholds": [],
      "title": "CPU Quota",
      "tooltip": {
        "shared": false,
        "sort": 2,
        "value_type": "individual"
      },
      "transform": "table",
      "type": "table-old",
      "xaxis": {
        "mode": "time",
        "show": true,
        "values": []
      },
      "yaxes": [
        {
          "format": "short",
          "logBase": 1,
          "min": 0,
          "show": true
        },
        {
          "format": "short",
          "logBase": 1,
          "show": false
        }
      ]
    },
    {
      "collapsed": false,
      "datasource": {
        "type": "prometheus",
        "uid": "prometheus"
      },
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 20
      },
      "id": 26,
      "panels": [],
      "targets": [
        {
          "datasource": {
            "type": "prometheus",
            "uid": "prometheus"
          },
          "refId": "A"
        }
      ],
      "title": "Memory",
      "type": "row"
    },
    {
      "aliasColors": {},
      "bars": false,
      "dashLength": 10,
      "dashes": false,
      "datasource": {
        "uid": "$datasource"
      },
      "fill": 10,
      "fillGradient": 0,
      "gridPos": {
        "h": 7,
        "w": 24,
        "x": 0,
        "y": 21
      },
      "hiddenSeries": false,
      "id": 9,
      "interval": "1m",
      "legend": {
        "alignAsTable": true,
        "avg": false,
        "current": false,
        "max": false,
        "min": false,
        "rightSide": true,
        "show": true,
        "total": false,
        "values": false
      },
      "lines": true,
      "linewidth": 0,
      "links": [],
      "nullPointMode": "null as zero",
      "options": {
        "alertThreshold": true
      },
      "percentage": false,
      "pluginVersion": "9.5.5",
      "pointradius": 5,
      "points": false,
      "renderer": "flot",
      "seriesOverrides": [],
      "spaceLength": 10,
      "stack": true,
      "steppedLine": false,
      "targets": [
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(container_memory_rss{job=\"kubelet\", metrics_path=\"/metrics/cadvisor\", cluster=\"$cluster\", container!=\"\"}) by (namespace)",
          "format": "time_series",
          "intervalFactor": 2,
          "legendFormat": "{{namespace}}",
          "refId": "A",
          "step": 10
        }
      ],
      "thresholds": [],
      "timeRegions": [],
      "title": "Memory Usage (w/o cache)",
      "tooltip": {
        "shared": false,
        "sort": 2,
        "value_type": "individual"
      },
      "type": "graph",
      "xaxis": {
        "mode": "time",
        "show": true,
        "values": []
      },
      "yaxes": [
        {
          "format": "bytes",
          "logBase": 1,
          "min": 0,
          "show": true
        },
        {
          "format": "short",
          "logBase": 1,
          "show": false
        }
      ],
      "yaxis": {
        "align": false
      }
    },
    {
      "collapsed": false,
      "datasource": {
        "type": "prometheus",
        "uid": "prometheus"
      },
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 28
      },
      "id": 27,
      "panels": [],
      "targets": [
        {
          "datasource": {
            "type": "prometheus",
            "uid": "prometheus"
          },
          "refId": "A"
        }
      ],
      "title": "Memory Requests",
      "type": "row"
    },
    {
      "aliasColors": {},
      "bars": false,
      "columns": [],
      "dashLength": 10,
      "dashes": false,
      "datasource": {
        "uid": "$datasource"
      },
      "fill": 1,
      "fontSize": "100%",
      "gridPos": {
        "h": 7,
        "w": 24,
        "x": 0,
        "y": 29
      },
      "id": 10,
      "interval": "1m",
      "legend": {
        "alignAsTable": true,
        "avg": false,
        "current": false,
        "max": false,
        "min": false,
        "rightSide": true,
        "show": true,
        "total": false,
        "values": false
      },
      "lines": true,
      "linewidth": 1,
      "links": [],
      "nullPointMode": "null as zero",
      "percentage": false,
      "pointradius": 5,
      "points": false,
      "renderer": "flot",
      "seriesOverrides": [],
      "showHeader": true,
      "sort": {
        "col": 0,
        "desc": true
      },
      "spaceLength": 10,
      "stack": false,
      "steppedLine": false,
      "styles": [
        {
          "alias": "Time",
          "align": "auto",
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "pattern": "Time",
          "type": "hidden"
        },
        {
          "alias": "Pods",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 0,
          "link": true,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down to pods",
          "linkUrl": "/d/85a562078cdf77779eaa1add43ccec1e/k8s-resources-namespace?var-datasource=$datasource&var-cluster=$cluster&var-namespace=$__cell_1",
          "pattern": "Value #A",
          "thresholds": [],
          "type": "number",
          "unit": "short"
        },
        {
          "alias": "Workloads",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 0,
          "link": true,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down to workloads",
          "linkUrl": "/d/a87fb0d919ec0ea5f6543124e16c42a5/k8s-resources-workloads-namespace?var-datasource=$datasource&var-cluster=$cluster&var-namespace=$__cell_1",
          "pattern": "Value #B",
          "thresholds": [],
          "type": "number",
          "unit": "short"
        },
        {
          "alias": "Memory Usage",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "link": false,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down",
          "linkUrl": "",
          "pattern": "Value #C",
          "thresholds": [],
          "type": "number",
          "unit": "bytes"
        },
        {
          "alias": "Memory Requests",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "link": false,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down",
          "linkUrl": "",
          "pattern": "Value #D",
          "thresholds": [],
          "type": "number",
          "unit": "bytes"
        },
        {
          "alias": "Memory Requests %",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "link": false,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down",
          "linkUrl": "",
          "pattern": "Value #E",
          "thresholds": [],
          "type": "number",
          "unit": "percentunit"
        },
        {
          "alias": "Memory Limits",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "link": false,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down",
          "linkUrl": "",
          "pattern": "Value #F",
          "thresholds": [],
          "type": "number",
          "unit": "bytes"
        },
        {
          "alias": "Memory Limits %",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "link": false,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down",
          "linkUrl": "",
          "pattern": "Value #G",
          "thresholds": [],
          "type": "number",
          "unit": "percentunit"
        },
        {
          "alias": "Namespace",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "link": true,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down to pods",
          "linkUrl": "/d/85a562078cdf77779eaa1add43ccec1e/k8s-resources-namespace?var-datasource=$datasource&var-cluster=$cluster&var-namespace=$__cell",
          "pattern": "namespace",
          "thresholds": [],
          "type": "number",
          "unit": "short"
        },
        {
          "alias": "",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "pattern": "/.*/",
          "thresholds": [],
          "type": "string",
          "unit": "short"
        }
      ],
      "targets": [
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(kube_pod_owner{job=\"kube-state-metrics\", cluster=\"$cluster\"}) by (namespace)",
          "format": "table",
          "instant": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "A",
          "step": 10
        },
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "count(avg(namespace_workload_pod:kube_pod_owner:relabel{cluster=\"$cluster\"}) by (workload, namespace)) by (namespace)",
          "format": "table",
          "instant": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "B",
          "step": 10
        },
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(container_memory_rss{job=\"kubelet\", metrics_path=\"/metrics/cadvisor\", cluster=\"$cluster\", container!=\"\"}) by (namespace)",
          "format": "table",
          "instant": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "C",
          "step": 10
        },
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(namespace_memory:kube_pod_container_resource_requests:sum{cluster=\"$cluster\"}) by (namespace)",
          "format": "table",
          "instant": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "D",
          "step": 10
        },
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(container_memory_rss{job=\"kubelet\", metrics_path=\"/metrics/cadvisor\", cluster=\"$cluster\", container!=\"\"}) by (namespace) / sum(namespace_memory:kube_pod_container_resource_requests:sum{cluster=\"$cluster\"}) by (namespace)",
          "format": "table",
          "instant": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "E",
          "step": 10
        },
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(namespace_memory:kube_pod_container_resource_limits:sum{cluster=\"$cluster\"}) by (namespace)",
          "format": "table",
          "instant": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "F",
          "step": 10
        },
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(container_memory_rss{job=\"kubelet\", metrics_path=\"/metrics/cadvisor\", cluster=\"$cluster\", container!=\"\"}) by (namespace) / sum(namespace_memory:kube_pod_container_resource_limits:sum{cluster=\"$cluster\"}) by (namespace)",
          "format": "table",
          "instant": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "G",
          "step": 10
        }
      ],
      "thresholds": [],
      "title": "Requests by Namespace",
      "tooltip": {
        "shared": false,
        "sort": 2,
        "value_type": "individual"
      },
      "transform": "table",
      "type": "table-old",
      "xaxis": {
        "mode": "time",
        "show": true,
        "values": []
      },
      "yaxes": [
        {
          "format": "short",
          "logBase": 1,
          "min": 0,
          "show": true
        },
        {
          "format": "short",
          "logBase": 1,
          "show": false
        }
      ]
    },
    {
      "collapsed": false,
      "datasource": {
        "type": "prometheus",
        "uid": "prometheus"
      },
      "gridPos": {
        "h": 1,
        "w": 24,
        "x": 0,
        "y": 36
      },
      "id": 28,
      "panels": [],
      "targets": [
        {
          "datasource": {
            "type": "prometheus",
            "uid": "prometheus"
          },
          "refId": "A"
        }
      ],
      "title": "Current Network Usage",
      "type": "row"
    },
    {
      "aliasColors": {},
      "bars": false,
      "columns": [],
      "dashLength": 10,
      "dashes": false,
      "datasource": {
        "uid": "$datasource"
      },
      "fill": 1,
      "fontSize": "100%",
      "gridPos": {
        "h": 7,
        "w": 24,
        "x": 0,
        "y": 37
      },
      "id": 11,
      "interval": "1m",
      "legend": {
        "alignAsTable": true,
        "avg": false,
        "current": false,
        "max": false,
        "min": false,
        "rightSide": true,
        "show": true,
        "total": false,
        "values": false
      },
      "lines": true,
      "linewidth": 1,
      "links": [],
      "nullPointMode": "null as zero",
      "percentage": false,
      "pointradius": 5,
      "points": false,
      "renderer": "flot",
      "seriesOverrides": [],
      "showHeader": true,
      "sort": {
        "col": 0,
        "desc": true
      },
      "spaceLength": 10,
      "stack": false,
      "steppedLine": false,
      "styles": [
        {
          "alias": "Time",
          "align": "auto",
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "pattern": "Time",
          "type": "hidden"
        },
        {
          "alias": "Current Receive Bandwidth",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "link": false,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down",
          "linkUrl": "",
          "pattern": "Value #A",
          "thresholds": [],
          "type": "number",
          "unit": "Bps"
        },
        {
          "alias": "Current Transmit Bandwidth",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "link": false,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down",
          "linkUrl": "",
          "pattern": "Value #B",
          "thresholds": [],
          "type": "number",
          "unit": "Bps"
        },
        {
          "alias": "Rate of Received Packets",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "link": false,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down",
          "linkUrl": "",
          "pattern": "Value #C",
          "thresholds": [],
          "type": "number",
          "unit": "pps"
        },
        {
          "alias": "Rate of Transmitted Packets",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "link": false,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down",
          "linkUrl": "",
          "pattern": "Value #D",
          "thresholds": [],
          "type": "number",
          "unit": "pps"
        },
        {
          "alias": "Rate of Received Packets Dropped",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "link": false,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down",
          "linkUrl": "",
          "pattern": "Value #E",
          "thresholds": [],
          "type": "number",
          "unit": "pps"
        },
        {
          "alias": "Rate of Transmitted Packets Dropped",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "link": false,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down",
          "linkUrl": "",
          "pattern": "Value #F",
          "thresholds": [],
          "type": "number",
          "unit": "pps"
        },
        {
          "alias": "Namespace",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "link": true,
          "linkTargetBlank": false,
          "linkTooltip": "Drill down to pods",
          "linkUrl": "/d/85a562078cdf77779eaa1add43ccec1e/k8s-resources-namespace?var-datasource=$datasource&var-cluster=$cluster&var-namespace=$__cell",
          "pattern": "namespace",
          "thresholds": [],
          "type": "number",
          "unit": "short"
        },
        {
          "alias": "",
          "align": "auto",
          "colors": [],
          "dateFormat": "YYYY-MM-DD HH:mm:ss",
          "decimals": 2,
          "pattern": "/.*/",
          "thresholds": [],
          "type": "string",
          "unit": "short"
        }
      ],
      "targets": [
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(irate(container_network_receive_bytes_total{job=\"kubelet\", metrics_path=\"/metrics/cadvisor\", cluster=\"$cluster\", namespace=~\".+\"}[$__rate_interval])) by (namespace)",
          "format": "table",
          "instant": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "A",
          "step": 10
        },
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(irate(container_network_transmit_bytes_total{job=\"kubelet\", metrics_path=\"/metrics/cadvisor\", cluster=\"$cluster\", namespace=~\".+\"}[$__rate_interval])) by (namespace)",
          "format": "table",
          "instant": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "B",
          "step": 10
        },
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(irate(container_network_receive_packets_total{job=\"kubelet\", metrics_path=\"/metrics/cadvisor\", cluster=\"$cluster\", namespace=~\".+\"}[$__rate_interval])) by (namespace)",
          "format": "table",
          "instant": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "C",
          "step": 10
        },
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(irate(container_network_transmit_packets_total{job=\"kubelet\", metrics_path=\"/metrics/cadvisor\", cluster=\"$cluster\", namespace=~\".+\"}[$__rate_interval])) by (namespace)",
          "format": "table",
          "instant": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "D",
          "step": 10
        },
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(irate(container_network_receive_packets_dropped_total{job=\"kubelet\", metrics_path=\"/metrics/cadvisor\", cluster=\"$cluster\", namespace=~\".+\"}[$__rate_interval])) by (namespace)",
          "format": "table",
          "instant": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "E",
          "step": 10
        },
        {
          "datasource": {
            "uid": "$datasource"
          },
          "expr": "sum(irate(container_network_transmit_packets_dropped_total{job=\"kubelet\", metrics_path=\"/metrics/cadvisor\", cluster=\"$cluster\", namespace=~\".+\"}[$__rate_interval])) by (namespace)",
          "format": "table",
          "instant": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "F",
          "step": 10
        }
      ],
      "thresholds": [],
      "title": "Current Network Usage",
      "tooltip": {
        "shared": false,
        "sort": 2,
        "value_type": "individual"
      },
      "transform": "table",
      "type": "table-old",
      "xaxis": {
        "mode": "time",
        "show": true,
        "values": []
      },
      "yaxes": [
        {
          "format": "short",
          "logBase": 1,
          "min": 0,
          "show": true
        },
        {
          "format": "short",
          "logBase": 1,
          "show": false
        }
      ]
    }
  ],
  "refresh": "10s",
  "schemaVersion": 38,
  "style": "dark",
  "tags": [
    "kubernetes-mixin"
  ],
  "templating": {
    "list": [
      {
        "current": {
          "selected": false,
          "text": "default",
          "value": "default"
        },
        "hide": 0,
        "includeAll": false,
        "label": "Data Source",
        "multi": false,
        "name": "datasource",
        "options": [],
        "query": "prometheus",
        "refresh": 1,
        "regex": "",
        "skipUrlSync": false,
        "type": "datasource"
      },
      {
        "current": {
          "isNone": true,
          "selected": false,
          "text": "None",
          "value": ""
        },
        "datasource": {
          "type": "prometheus",
          "uid": "$datasource"
        },
        "definition": "",
        "hide": 2,
        "includeAll": false,
        "multi": false,
        "name": "cluster",
        "options": [],
        "query": "label_values(up{job=\"kubelet\", metrics_path=\"/metrics/cadvisor\"}, cluster)",
        "refresh": 2,
        "regex": "",
        "skipUrlSync": false,
        "sort": 1,
        "tagValuesQuery": "",
        "tagsQuery": "",
        "type": "query",
        "useTags": false
      }
    ]
  },
  "time": {
    "from": "now-1h",
    "to": "now"
  },
  "timepicker": {
    "refresh_intervals": [
      "5s",
      "10s",
      "30s",
      "1m",
      "5m",
      "15m",
      "30m",
      "1h",
      "2h",
      "1d"
    ],
    "time_options": [
      "5m",
      "15m",
      "1h",
      "6h",
      "12h",
      "24h",
      "2d",
      "7d",
      "30d"
    ]
  },
  "timezone": "utc",
  "title": "Kubernetes / Compute Resources / Cluster",
  "uid": "efa86fd1d0c121a26444b636a3f509a8",
  "version": 1,
  "weekStart": ""
}


